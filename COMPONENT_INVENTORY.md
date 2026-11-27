# COMPONENT_INVENTORY.md — جرد المكونات (موجودة / مضافة / محذوفة)

> الإصدار المرجعي: Chromium **158.0.8127.89** (`1de57fa19722fa6d6841d4f596c394d015580656`)، V8 **15.8.62.31**.
> الحالة بعد المهمة: **~71,450 ملفاً**، **~963 MB** شجرة العمل. أُضيف **~16,750 ملفاً** وأُزيل **4,884 ملفاً + 10 روابط مكسورة**.

## أ. المكونات الأساسية الموجودة وأُبقي عليها (تحقق بالملفات)

| المكون | المسار | الحالة | الوظيفة |
|---|---|---|---|
| Blink Core | `blink/renderer/core` | موجود | HTML/DOM/CSS/Style/LayoutNG/Paint/SVG/Forms/Events/Editing/Loader/Fetch/Workers/Script/Streams/Animation |
| Blink Modules | `blink/renderer/modules` | موجود + مُستكمل | WebGL/WebAudio/WebCodecs/WebSockets/WebTransport/ServiceWorker/IndexedDB/CacheStorage/Canvas + المضافة أدناه |
| Blink Platform | `blink/renderer/platform` | موجود + مُستكمل | fonts/text(BiDi)/graphics/loader/network/blob/scheduler/bindings/heap(Oilpan)/wtf |
| V8 | `v8/src`, `v8/include` | موجود كامل | JavaScript (Ignition/Sparkplug/Maglev/TurboFan) + WebAssembly + Oilpan |
| Skia | `skia/` | موجود + مُستكمل | Ganesh/Graphite/skcms/skshaper/skparagraph/svg + خلفية Dawn |
| ANGLE | `angle/` | موجود | OpenGL ES 2/3 + WebGL 1/2 + ترجمة GLSL |
| SwiftShader | `third_party/swiftshader` | موجود | رسم برمجي (Vulkan/GLES) |
| ICU | `icu/` | موجود كامل | Unicode/RTL/BiDi/تشكيل عربي |
| HarfBuzz | `harfbuzz/` | موجود | تشكيل OpenType |
| FreeType | `third_party/freetype` | موجود | تحميل الخطوط |
| net | `net/` | موجود + مُستكمل | HTTP/1.1–3/TLS/cookies/cache/QUIC/WebSocket + cert/proxy/reporting |
| media | `media/` | موجود + مُستكمل | ffmpeg/libvpx/libaom/dav1d/opus/flac + capture/webrtc/cdm |
| gpu | `gpu/` | موجود + مُستكمل | command_buffer/GLES2/ipc/vulkan + webgpu/dawn |
| cc / viz | `cc/`, `viz/` | موجود + مُستكمل | مركّب الطبقات/الأسطح + cc/metrics |
| mojo / ipc / gin | `mojo/`, `ipc/`, `gin/` | موجود | IPC بين العمليات + ربط V8 |
| base / sandbox / url / crypto / sql / storage / dbus | respective | موجود | البنية التأسيسية |
| ui | `ui/` | موجود | gfx/gl/ozone/aura/events/compositor/display/platform_window |
| services | `services/` | موجود + مُستكمل | network/viz/audio/data_decoder/device + metrics/media_session |
| components | `components/` | موجود + مُستكمل | webcrypto/viz/storage/services + webrtc/push_messaging/crash |
| content | `content/` | موجود + مُستكمل | renderer/gpu/child/common/renderer_host/worker_host/service_worker + permissions/notifications/geolocation/push |

## ب. المكونات المضافة (استعادة من المصدر الرسمي المطابق)

### WebGPU / Dawn
| المكون | المصدر | ملفات |
|---|---|---:|
| Dawn (native + Tint + utils + include + generator) | `dawn.googlesource.com/dawn @ 6e245424` | ~2,464 |
| Blink WebGPU module | Chromium src | 218 |
| gpu/webgpu + command_buffer webgpu (client/common/service) | Chromium src | ~35 |
| gpu/config + gpu/ipc/service (webgpu) | Chromium src | 4 |
| Skia Graphite Dawn backend | `skia @ 3279352f` | 32 |
| SPIRV-Tools | `KhronosGroup/SPIRV-Tools @ 066042ec` | 841 |
| SPIRV-Cross | `KhronosGroup/SPIRV-Cross @ b8fcf307` | 4,321 |
| SPIRV-Headers (استكمال) | `KhronosGroup/SPIRV-Headers @ fbf86836` | +35 |
| Blink platform graphics/gpu (webgpu) | Chromium src | 12 |

### WebRTC + Media Capture
| المكون | المصدر | ملفات |
|---|---|---:|
| WebRTC (api/call/modules/pc/p2p/rtc_base/net/dcsctp…) | `webrtc.googlesource.com/src @ fb1c41a9` | ~3,232 |
| webrtc_overrides | Chromium src | 48 |
| libsrtp | `chromium/deps/libsrtp @ cd5d177b` | 45 |
| jsoncpp / crc32c | pinned DEPS | 94 |
| Blink peerconnection/mediastream/mediarecorder/mediacapturefromelement/webrtc | Chromium src | ~486 |
| Blink platform mediastream/peerconnection/webrtc/p2p/video_capture | Chromium src | ~155 |
| media/capture + media/webrtc | Chromium src | 290 |
| components/webrtc + blink public common/webrtc | Chromium src | 28 |
| public platform/web modules (mediastream/webrtc/video_capture) + mojom | Chromium src | ~27 |
| sframe (E2EE) | `cisco/sframe @ 6a37f061` | 24 |

### Geolocation / Notifications / Push / Permissions
| المكون | ملفات |
|---|---:|
| Blink core/geolocation (نُقلت من modules في 158) | 23 |
| services/device/geolocation + public mojom/cpp | 127 |
| content/browser/geolocation | 2 |
| Blink modules notifications/push_messaging/permissions | 85 |
| content/browser notifications/push_messaging/permissions | 42 |
| components/push_messaging | 8 |
| blink/public/mojom (notifications/push/permissions/mediastream/peerconnection) | 12 |

### التحقق من شهادات TLS (ضروري لـ HTTPS)
| المكون | ملفات |
|---|---:|
| net/cert + net/cert_net | 145 |
| net/data/ssl (chrome_root_store/root_stores/blocklist) | 132 |
| BoringSSL pki (src/pki + include/openssl/pki) | 74 |

### بنية تحتية مشتركة (كانت محذوفة وتحتاجها المكونات)
base/metrics (70)، services/metrics/public (22)، net/proxy_resolution (92)، net/reporting (35)، net/storage_access_api (1)، cc/metrics (71)، components/crash/core/common (20)، blink core/public origin_trials (10)، blink public common/metrics (2)، services/media_session/public/cpp (25)، media/cdm + api (94)، base/check_is_test (2)، audio_output_devices (3).

### تحسينات ML الصوتية الاختيارية (WebRTC)
tflite-lite core (~829) + tensorflow/core/platform (126) + core/lib (44) + mlir/lite core (24)، farmhash (70)، flatbuffers (518)، gemmlowp (114)، ruy (111). *(انظر MISSING_COMPONENTS.md للتحفظات حول الأجزاء الاختيارية.)*

## ج. المكونات المحذوفة في هذه المهمة

| الفئة | العدد |
|---|---:|
| منظومة بناء Chromium (GN/gclient/infra/build/codegen) | 2,963 |
| اختبارات/fuzzers/ربط Node.js/أجزاء ML اختيارية (rnn_vad/tflite-experimental) | 1,911 |
| روابط رمزية مكسورة | 10 |
| **الإجمالي** | **4,884 + 10** |

التفاصيل الكاملة في [`REMOVED_FILES.md`](REMOVED_FILES.md) و[`docs/logs/`](docs/logs/).

## د. ملاحظات
- لا توجد مكونات مكررة فعلية؛ الروابط الرمزية (`third_party/{blink,angle,skia,icu} → الجذر`, `components/viz → ../viz`) تمنع الازدواج.
- `blink/web_tests` و`blink/perf_tests` المتبقية = ملفات تراخيص فقط (50 ملفاً) — محفوظة.
- `v8/test` المتبقي (52KB) اختبارات أساسية — محفوظة.
- libxslt: المصدر الأساسي مقلم من خط الأساس (بقيت config.h فقط)؛ أُعيد ترخيص `Copyright`. دعم XSLT غير مكتمل (ميزة ويب قديمة اختيارية).
