# WEB_PLATFORM_SUPPORT.md — مصفوفة دعم واجهات الويب

> **منهجية الصدق:** «موجود» يعني أن الملفات المصدرية والاعتماديات الأساسية موجودة وتم التحقق منها ساكنياً. **لا يُدّعى توافق تشغيلي كامل** لأنه لم يُنفّذ أي Build/Compile أو اختبار تشغيل (ممنوع في هذه المهمة). مستوى الاكتمالrunning يتطلب تحقق الـ Embedder المستقبلي.
>
> مستويات الاكتمال: **كامل مصدرياً** (المحرك + الربط + الاعتماديات موجودة) / **موجود جزئياً** (بعض الاعتماديات مقطوعة/اختيارية) / **غير متحقق** (يحتاج اختبار تشغيل).

## 1. HTML / DOM / CSS

| الواجهة | الحالة | المستوى | الملفات/المسار | الاعتماديات | الإجراء |
|---|---|---|---|---|---|
| HTML Parser / DOM | موجود | كامل مصدرياً | `blink/renderer/core/html`, `core/dom` | V8, ICU | أُبقي |
| Shadow DOM / Custom Elements / Templates | موجود | كامل مصدرياً | `core/dom` | — | أُبقي |
| MutationObserver | موجود | كامل مصدرياً | `core/dom/mutation_observer*` | — | أُبقي |
| ResizeObserver / IntersectionObserver | موجود | كامل مصدرياً | `core/resize_observer`, `core/intersection_observer` | — | أُبقي |
| Selection / Range API | موجود | كامل مصدرياً | `core/editing` | — | أُبقي |
| DOM Events / Event Loop | موجود | كامل مصدرياً | `core/events`, `core/scheduler`, `platform/scheduler` | base | أُبقي |
| Web Components | موجود | كامل مصدرياً | `core/dom`, `core/html` | — | أُبقي |
| CSS Parser / CSSOM / Style / Selector | موجود | كامل مصدرياً | `core/css`, `core/style` | — | أُبقي |
| Flexbox / Grid / LayoutNG | موجود | كامل مصدرياً | `core/layout` | — | أُبقي |
| CSS Variables / Container/Media Queries | موجود | كامل مصدرياً | `core/css` | — | أُبقي |
| Animations / Transitions / Transforms / Filters | موجود | كامل مصدرياً | `core/animation`, `core/css`, `core/paint` | cc | أُبقي |
| Pseudo Elements / Fonts / Modern CSS | موجود | كامل مصدرياً | `core/css`, `platform/fonts` | HarfBuzz/FreeType/ICU | أُبقي |

## 2. JavaScript / WebAssembly (V8)

| الواجهة | الحالة | المستوى | المسار | الإجراء |
|---|---|---|---|---|
| JavaScript Engine / ECMAScript | موجود | كامل مصدرياً | `v8/src`, `v8/include` | أُبقي |
| JIT (Ignition/Sparkplug/Maglev/TurboFan) | موجود | كامل مصدرياً | `v8/src/{interpreter,baseline,maglev,compiler}` | أُبقي |
| Garbage Collection (Oilpan/Heap) | موجود | كامل مصدرياً | `v8/src/heap`, `blink/renderer/platform/heap` | أُبقي |
| Modules / Promises / Async-Await | موجود | كامل مصدرياً | `v8/src`, `core/script` | أُبقي |
| WebAssembly (Core/SIMD/Threads/Memory/RefTypes/EH) | موجود | كامل مصدرياً | `v8/src/wasm` | أُبقي |
| Workers / SharedArrayBuffer / Structured Clone | موجود | كامل مصدرياً | `core/workers`, `bindings/core/v8/serialization` | أُبقي |
| ربط V8 بـ Web Platform | موجود | كامل مصدرياً | `gin`, `blink/renderer/bindings`, `platform/bindings` | أُبقي (مولّدات IDL أُزيلت كبيانات بناء؛ .idl محفوظة) |

## 3. Graphics / WebGL / WebGPU

| الواجهة | الحالة | المستوى | المسار | الإجراء |
|---|---|---|---|---|
| Skia (Ganesh/Graphite) / Rasterization | موجود | كامل مصدرياً | `skia/` | أُبقي |
| ANGLE / Hardware Acceleration | موجود | كامل مصدرياً | `angle/` | أُبقي |
| GPU Process / Compositor / Surface/Texture/Memory Mgmt | موجود | كامل مصدرياً | `gpu/`, `cc/`, `viz/` | أُبقي |
| **WebGL 1.0 / 2.0** (GLSL/Textures/FBO/Shaders/Buffers/Extensions) | موجود | كامل مصدرياً | `blink/renderer/modules/webgl`, `gpu/command_buffer`, ANGLE | أُبقي |
| **WebGPU** (Adapter/Device/CommandBuffers/Compute/RenderPipelines/Buffers/Textures) | **مستكمل** | كامل مصدرياً | `blink/renderer/modules/webgpu`, `third_party/dawn` (native+Tint), `gpu/webgpu`, `gpu/command_buffer/*/webgpu*`, Skia Graphite/Dawn, SPIRV-Tools/Cross | **أُضيف من المصدر الرسمي** |

## 4. Web Platform APIs

| الواجهة | الحالة | المستوى | المسار | الإجراء |
|---|---|---|---|---|
| Fetch API / XMLHttpRequest | موجود | كامل مصدرياً | `core/fetch`, `core/xmlhttprequest`, net | أُبقي |
| WebSocket / EventSource | موجود | كامل مصدرياً | `modules/websockets`, `modules/eventsource` | أُبقي |
| Web Workers / Service Workers | موجود | كامل مصدرياً | `core/workers`, `modules/service_worker`, `content/browser/service_worker` | أُبقي |
| Cache API / IndexedDB / Web Storage | موجود | كامل مصدرياً | `modules/cache_storage`, `modules/indexeddb`, `modules/storage`, storage/ | أُبقي |
| BroadcastChannel / MessageChannel | موجود | كامل مصدرياً | `modules/broadcastchannel`, `core/messaging` | أُبقي |
| **WebRTC** | **مستكمل** | كامل مصدرياً | `modules/peerconnection`, `third_party/webrtc`, media/webrtc, libsrtp | **أُضيف** |
| WebCodecs | موجود | كامل مصدرياً | `modules/webcodecs`, media/ | أُبقي |
| Web Audio API | موجود | كامل مصدرياً | `modules/webaudio`, `platform/audio` | أُبقي |
| **Media Capture (getUserMedia/getDisplayMedia)** | **مستكمل** | كامل مصدرياً | `modules/mediastream`, `media/capture`, `platform/video_capture` | **أُضيف** |
| MediaRecorder | مستكمل | كامل مصدرياً | `modules/mediarecorder` | أُضيف |
| Canvas 2D / OffscreenCanvas | موجود | كامل مصدرياً | `modules/canvas`, `core/offscreencanvas`, `platform/graphics` | أُبقي |
| File API / Blob / Streams API | موجود | كامل مصدرياً | `core/fileapi`, `core/streams`, `platform/blob` | أُبقي |
| Clipboard API | موجود | كامل مصدرياً | `modules/clipboard`, `core/clipboard` | أُبقي |
| Fullscreen API | موجود | كامل مصدرياً | `core/fullscreen` | أُبقي |
| Pointer / Touch / Keyboard Events / Drag-Drop | موجود | كامل مصدرياً | `core/events`, `core/input`, `core/editing` | أُبقي |
| **Notifications** | **مستكمل** | موجود جزئياً (backend للـ Embedder) | `modules/notifications`, `content/browser/notifications` | **أُضيف** |
| **Push API** | **مستكمل** | موجود جزئياً (backend للـ Embedder) | `modules/push_messaging`, `content/browser/push_messaging`, `components/push_messaging` | **أُضيف** |
| **Geolocation** | **مستكمل** | كامل مصدرياً | `core/geolocation`, `services/device/geolocation`, `content/browser/geolocation` | **أُضيف** |
| **Permissions API** | **مستكمل** | كامل مصدرياً | `modules/permissions`, `content/browser/permissions` | **أُضيف** |
| URL / URLSearchParams / URLPattern | موجود | كامل مصدرياً | `core/url`, `core/url_pattern`, url/ | أُبقي |
| Performance API | موجود | كامل مصدرياً | `core/timing` | أُبقي |
| Crypto API (WebCrypto) | موجود | كامل مصدرياً | `modules/crypto`, `components/webcrypto`, BoringSSL | أُبقي |
| Web Animations API | موجود | كامل مصدرياً | `core/animation` | أُبقي |
| ResizeObserver / MutationObserver / IntersectionObserver | موجود | كامل مصدرياً | core/ | أُبقي |
| WebTransport | موجود | كامل مصدرياً | `modules/webtransport`, net/quic | أُبقي |
| Encrypted Media (EME) | موجود | موجود جزئياً (CDM للـ Embedder) | `modules/encryptedmedia`, `media/cdm` | أُبقي + أُضيف media/cdm/api |
| FileSystemAccess / OPFS | موجود | كامل مصدرياً | `modules/file_system_access`, `modules/filesystem`, storage | أُبقي |
| WebSockets/Compression/Beacon/Buckets/Locks/NetInfo | موجود | كامل مصدرياً | modules/ | أُبقي |

## 5. واجهات غير مدعومة (محذوفة عن قصد — لا تحتاجها تطبيقات الويب الأساسية)

WebXR/VR، Bluetooth/USB/Serial/HID/NFC/MIDI/SmartCard/Sensor (عتاد)، WebAuthn/FIDO، Payment Request، Presentation/RemotePlayback، Idle Detection، WebShare/Contacts، DevTools UI، التصفح الخارجي/Safe Browsing/التتبع. *(يمكن إعادة جلبها اختيارياً من upstream لاحقاً.)*

## 6. توافق أطر تطبيقات الويب

| الإطار | المتطلبات | الحالة المصدرية |
|---|---|---|
| React / React DOM / Next.js (client) | DOM, Custom Elements, fetch, ES Modules, Event Loop, CSS | موجود مصدرياً |
| Vue / Nuxt (client) | DOM, Proxy(V8), fetch, CSS, History API | موجود مصدرياً |
| Angular | DOM, Zone.js(V8), fetch, CSS, Web Components | موجود مصدرياً |
| Svelte / SolidJS | DOM, ES Modules, reactive (V8), CSS | موجود مصدرياً |
| Astro (client hydration) | DOM, ES Modules, fetch, CSS | موجود مصدرياً |
| SPA / SSR-after-hydration / TypeScript→JS | DOM + V8 + fetch + History | موجود مصدرياً |
| Web Components / Canvas / WebGL / WebGPU apps | المكوّنات أعلاه | موجود/مستكمل مصدرياً |

> **تنبيه صدق:** التوافق التشغيلي الفعلي مع هذه الأطر **غير متحقق** في هذه المهمة (لا بناء/تشغيل). المصفوفة تثبت **وجود البنية المصدرية والاعتماديات** فقط. التحقق التشغيلي مسؤولية مرحلة البناء المستقبلية.
