# DEPENDENCY_MAP.md — خريطة الاعتماديات بين المكونات

> مبنية على فحص `#include` الساكن (342,227 تضميناً محلولاً) ومصادر Chromium الرسمية. لا تتضمن أي بناء.

## 1. المخطط الطبقي العام

```
┌─────────────────────────────────────────────────────────────────────┐
│  Embedder / Ultra Desktop Framework (مستقبلاً — غير موجود في هذه المهمة)   │
│  ينشئ: BrowserContext, WebContents, نافذة أصلية, حلقة أحداث, app://        │
└───────────────┬─────────────────────────────────────────────────────┘
                │ content/public API
┌───────────────▼─────────────────────────────────────────────────────┐
│  content/  (renderer_host, browser, gpu, child, common, utility)       │
│  يربط: Blink ↔ الشبكة ↔ GPU ↔ التخزين ↔ الوسائط ↔ الأذونات                │
└──┬──────────────┬───────────────┬──────────────┬─────────────────────┘
   │              │               │              │
┌──▼─────────┐ ┌──▼──────────┐ ┌──▼─────────┐ ┌──▼──────────────────────┐
│ Blink      │ │ services/   │ │ gpu/       │ │ media/                  │
│ renderer/  │ │ network,viz,│ │ command_   │ │ capture,webrtc,cdm,     │
│ core,mods, │ │ audio,device│ │ buffer,    │ │ ffmpeg,filters,renderers│
│ platform   │ │ metrics     │ │ webgpu,vk  │ │                         │
└──┬───┬───┬─┘ └──┬──────┬─── └──┬────┬──┘ └──┬──────────────────────┘
   │   │   │      │      │        │    │        │
┌──▼ ┌▼──┐ ▼───┐ ▼───┐ ▼───┐ ┌▼──┐ ┌▼─────┐ ┌▼──────────────────┐
│V8 │ │Skia│ │net │ │cc  │ │viz │ │ANGLE│ │Dawn │ │WebRTC             │
│gin│ │    │ │    │ │    │ │    │ │    │ │Tint │ │(pc,p2p,modules,   │
│   │ │    │ │    │ │    │ │    │ │    │ │     │ │ rtc_base,dcsctp)  │
└─┬─┘ └─┬──┘ └─┬──┘ └─┬──┘ └─┬──┘ └─┬──┘ └─┬─── └─┬────────────────┘
  │     │      │      │      │      │      │       │
┌─▼─────▼──────▼──────▼──────▼──────▼──────▼───────▼─────────────────┐
│ base / mojo / ipc / sandbox / url / crypto / sql / storage / ui      │
│ third_party: ICU, HarfBuzz, FreeType, BoringSSL, zlib, Abseil,        │
│ Protobuf, Perfetto, SPIRV-*, Vulkan-*, libyuv, opus, libvpx, …        │
└─────────────────────────────────────────────────────────────────────┘
```

## 2. اعتماديات المكونات الحرجة

| المكون | يعتمد على | ملاحظات |
|---|---|---|
| **Blink core** | V8 (bindings), Skia (paint), net (loader), cc/viz (compositing), ICU/HarfBuzz/FreeType (text), base/mojo | LayoutNG + CSS كامل |
| **Blink modules/webgpu** | Dawn (wire/native), gpu/command_buffer/webgpu, gpu/webgpu, Skia Graphite/Dawn, SPIRV-Tools/Cross | مسار WebGPU كامل |
| **Dawn/Tint** | Abseil, Protobuf, Perfetto, Vulkan-Headers, SPIRV-*, partition_alloc, fp16/highway/fast_float/dragonbox/simdutf | معظمها موجود؛ مولّدات codegen أُزيلت (بيانات القوالب محفوظة) |
| **Blink modules/peerconnection** | WebRTC, Blink platform/{peerconnection,mediastream,webrtc,p2p}, media/webrtc, components/webrtc, libsrtp, BoringSSL | مسار WebRTC كامل |
| **WebRTC** | Abseil, BoringSSL, libyuv, opus, libvpx, libaom, dav1d, jsoncpp, crc32c, libsrtp, net/dcsctp (داخلي), webrtc_overrides | pffft/rnnoise (rnn_vad) معطّلة كما في Chromium |
| **media/capture** | WebRTC (video), ui/gfx, content/browser/renderer_host/media, services/audio | getUserMedia/getDisplayMedia |
| **net/cert** | BoringSSL pki, net/base, net/data/ssl (root stores), base/metrics | التحقق من TLS |
| **gpu/command_buffer** | ANGLE, Skia, Dawn, ui/gl, ui/gfx, base/metrics, cc | GLES2 + WebGPU decoders |
| **content/browser** | net, storage, media, gpu, services/*, components/{permissions,push_messaging,crash}, base/metrics | المضيفون |
| **services/network** | net, mojo, base, components/{network_session_configurator,cookie_config} | خدمة الشبكة |
| **cc / viz** | Skia, gpu, ui/gfx, base/metrics, mojo | التركيب |
| **V8** | base, gin, partition_alloc, ICU, zlib | مستقل ذاتياً |
| **Skia** | ICU, HarfBuzz, FreeType, libpng/jpeg/webp, Dawn (Graphite), Vulkan-Headers, wuffs, highway | الرسم |

## 3. حالة حل الاعتماديات (الفحص النهائي)

| التصنيف | التكرارات | الفريد | المعنى |
|---|---:|---:|---|
| **محلول** | 342,227 | — | موجود في الشجرة (عبر الجذر أو جذور `-I` للمكتبات) |
| **مولّد وقت البناء** | 14,071 | 3,612 | `*.mojom.h`, `*.pb.h`, `*buildflags.h`, bindings V8، CSS/HTML names — تُنتج بواسطة codegen المستقبلي (طبيعي غيابها في المصدر الخام) |
| **أطر اختبار** | 440 | 129 | gtest/gmock غير مضمّنة (اختبارات) |
| **منصات محذوفة** | 627 | 174 | Android/iOS/ChromeOS/Fuchsia |
| **قطوع متعمدة** | 967 | 349 | DevTools/ميزات متصفح (موثّقة في CUT_DEPS.md) |
| **نقص متبقٍ** | 1,567 | 1,245 | ذيل اختياري (أجزاء tflite/opus/subzero/clspv، X11 ثانوي) — انظر MISSING_COMPONENTS.md |

## 4. الروابط الرمزية الحافظة للمسارات

`third_party/blink → ../blink`, `third_party/angle → ../angle`, `third_party/skia → ../skia`, `third_party/icu → ../icu`, `third_party/harfbuzz-ng/src → ../../harfbuzz`, `components/viz → ../viz`. جميعها سليمة وتُحلّ مسارات `#include` الرسمية.
