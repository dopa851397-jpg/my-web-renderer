# RUNTIME_ARCHITECTURE.md — التصور المعماري لمحرك Runtime مستقل

> الهدف: قاعدة مصدرية لتشغيل تطبيقات الويب (React/Vue/Angular/Svelte/Next/Nuxt/Solid/Astro…) كتطبيقات حقيقية **دون واجهة متصفح** (لا تبويبات/شريط عنوان/إشارات/سجل). هذه المهمة **تجهيز المصدر فقط** — لا بناء ولا تنفيذ.

## 1. المبدأ المعماري

المحرك يفصل **طبقة Embedder** (التي سيوفرها Ultra Desktop Framework مستقبلاً) عن **محرك الويب** (هذا المستودع). لا يعتمد المحرك على تشغيل Chrome أو واجهاته. نقطة الدخول المستقبلية هي `content/public` API:

- ينشئ الـ Embedder: `BrowserMainParts`, `ContentMainRunner`, `BrowserContext`, `WebContents`، نافذة أصلية عبر `ui/ozone`/`aura`، وحلقة أحداث.
- يحمّل أصول التطبيق محلياً عبر مخطط `app://` (يدعمه `url/` + `content/browser` URL loader factories) ويتصل بخادمه الخاص عبر `fetch`/`XHR`/`WebSocket`/`WebTransport`.
- يرسم التطبيق واجهته بالكامل بـ HTML/CSS/Canvas/WebGL/WebGPU.

## 2. الطبقات

| الطبقة | المكونات | الدور |
|---|---|---|
| **Embedder (مستقبلي)** | خارج هذا المستودع | نافذة، حلقة أحداث، تحميل app://، تكامل OS |
| **Content** | `content/{browser,renderer,gpu,child,common,utility,renderer_host,worker_host,service_worker}` | إدارة العمليات، التنقل، المضيفون، الأذونات |
| **Blink** | `blink/renderer/{core,modules,platform,bindings,controller}` + `blink/public` | DOM/CSS/Layout/Paint/JS bindings/Web APIs |
| **JS/Wasm** | `v8/`, `gin/` | تنفيذ JavaScript وWebAssembly |
| **Graphics** | `skia/`, `angle/`, `gpu/`, `cc/`, `viz/`, `third_party/{dawn,swiftshader,spirv-*,vulkan-*}` | رسم 2D مسرّع، WebGL، WebGPU، التركيب |
| **Media** | `media/`, `third_party/{ffmpeg,libvpx,libaom,dav1d,opus,flac,libwebm}`, `services/audio` | صوت/فيديو/WebCodecs/WebAudio/capture |
| **Realtime** | `third_party/{webrtc,webrtc_overrides,libsrtp,sframe}`, `media/{capture,webrtc}`, `components/webrtc` | WebRTC/getUserMedia |
| **Network** | `net/`, `services/network`, `net/third_party/quiche` | HTTP/1.1–3/TLS/QUIC/WebSocket/cert |
| **Storage** | `storage/`, `sql/`, `components/services/storage`, `third_party/{sqlite,leveldatabase}` | IndexedDB/CacheStorage/Blob/OPFS/localStorage |
| **Foundation** | `base/`, `mojo/`, `ipc/`, `sandbox/`, `url/`, `crypto/`, `ui/`, `dbus/` | خيوط/ذاكرة/IPC/عزل/نوافذ/أحداث |
| **Text/i18n** | `icu/`, `harfbuzz/`, `third_party/{freetype,fontconfig}` | Unicode/RTL/تشكيل/خطوط |

## 3. مسارات التشغيل الأساسية

### تحميل وعرض تطبيق ويب
```
app://index.html → content URLLoader → Blink HTML Parser → DOM
  → CSS Parser → Style Engine → LayoutNG → Paint → cc LayerTree
  → viz DisplayCompositor → Skia (Ganesh/Graphite) → GPU (ANGLE/Dawn) → Surface
```

### تنفيذ JavaScript
```
Blink ScriptLoader → V8 Isolate (gin) → Ignition/Sparkplug/Maglev/TurboFan
  → Web APIs عبر bindings (IDL مولّد) → Event Loop (Blink scheduler + base::RunLoop)
```

### WebGL / WebGPU
```
WebGL: Blink canvas → gpu/command_buffer GLES2 decoder → ANGLE → GL/Vulkan
WebGPU: Blink modules/webgpu → Dawn wire → gpu WebGPU decoder → Dawn native → Vulkan/Metal/D3D12
        WGSL → Tint → SPIR-V/MSL/HLSL ; Skia Graphite/Dawn للرسم
```

### WebRTC
```
getUserMedia → Blink mediastream → media/capture → audio/video devices
RTCPeerConnection → Blink peerconnection → WebRTC (pc/p2p/modules) → SRTP (libsrtp) / SCTP (net/dcsctp)
```

## 4. ما لا يحتويه المحرك (عن قصد)

لا تبويبات، لا شريط عنوان، لا إشارات مرجعية، لا سجل تصفح، لا واجهة إعدادات متصفح، لا مزامنة/حسابات متصفح، لا Safe Browsing، لا إضافات، لا DevTools UI (أُبقي على `ConsoleMessage` للتصحيح الأساسي)، لا منصات Android/iOS/ChromeOS/Fuchsia.

## 5. الفجوات المعمارية المتبقية (للـ Embedder المستقبلي)

- **نظام بناء مستقل**: أُزيلت منظومة Chromium؛ يجب على الـ Embedder توفير بناء + codegen (mojom/idl/json5/buildflags).
- **طبقة Embedder فعلية**: `ContentMainDelegate`, `ContentBrowserClient`, `ContentRendererClient` — غير موجودة (كانت في chrome/ المحذوف)؛ يكتبها الـ Embedder.
- **خدمة Push backend**: واجهات Blink/mojom موجودة؛ الـ Embedder يوفّر توصيل Push فعلي.
- **DevTools**: محذوف؛ يمكن إعادة جلبه اختيارياً للتطوير.

انظر [`MISSING_COMPONENTS.md`](MISSING_COMPONENTS.md) و[`WEB_PLATFORM_SUPPORT.md`](WEB_PLATFORM_SUPPORT.md).
