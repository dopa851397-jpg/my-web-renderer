# PROJECT_AUDIT.md — تدقيق حالة المستودع قبل التعديل وبعده

> المرحلة الأولى من مهمة تحويل `my-web-renderer` إلى قاعدة Runtime مستقلة لتشغيل تطبيقات الويب.
> هذا القسم يوثّق الحالة **قبل** أي تعديل (خط الأساس). يُستكمل قسم «بعد التعديل» في نهاية المهمة.

## 1. هوية المستودع والإصدار

| البند | القيمة |
|---|---|
| المستودع | `dopa851397-jpg/my-web-renderer` |
| الفرع الافتراضي | `main` (وفرع `main-pruned` يشير لنفس الـ Commit) |
| الـ Tags | لا توجد |
| Commit خط الأساس | `2ce4bd7bc838890c304c21239117c6876668f490` — «web-app-only baseline» |
| سجل Git | Commit واحد فقط (لا تاريخ تقليم متعدد المراحل داخل Git) |
| إصدار Chromium | **158.0.8127.89** |
| Commit المصدر الرسمي | `1de57fa19722fa6d6841d4f596c394d015580656` |
| إصدار V8 | 15.8.62.31 (`v8/include/v8-version.h`) |
| المرجع | CEF 158.0.6 (حسب وصف المستودع) |

## 2. المقاييس قبل التعديل

| المقياس | القيمة |
|---|---:|
| الملفات المتتبعة في Git | **59,545** (منها 30 رابطاً رمزياً) |
| الملفات العادية | 59,515 |
| حجم شجرة العمل | **849.59 MB** (890,860,647 بايت) |
| حجم `.git` | 188 MB (حزمة 180.16 MiB) |
| حجم المستودع على GitHub | 178,687 KB |
| ملفات التراخيص المحفوظة | 313 (`LICENSE`/`COPYING`/`NOTICE`) |

### التوزيع حسب المجلد الجذري (قبل)

| المجلد | ملفات | حجم |
|---|---:|---:|
| third_party | 11,423 | 259.42 MB |
| blink | 12,722 | 83.90 MB |
| icu | 5,780 | 127.07 MB |
| v8 | 3,571 | 69.57 MB |
| skia | 3,464 | 50.72 MB |
| angle | 2,260 | 41.29 MB |
| net | 2,863 | 33.51 MB |
| content | 2,638 | 23.32 MB |
| ui | 2,757 | 18.09 MB |
| media | 1,704 | 13.08 MB |
| base | 2,120 | 13.30 MB |
| gpu | 858 | 10.62 MB |
| components | 2,009 | 9.21 MB |
| services | 1,514 | 7.18 MB |
| harfbuzz | 574 | 6.99 MB |
| cc | 694 | 5.90 MB |
| viz | 536 | 3.99 MB |
| mojo | 774 | 3.83 MB |
| sandbox | 381 | 1.80 MB |
| build | 245 | 1.65 MB |
| storage | 232 | 1.64 MB |
| url | 76 | 0.53 MB |
| crypto | 94 | 0.53 MB |
| sql | 37 | 0.38 MB |
| dbus | 31 | 0.31 MB |
| gin | 74 | 0.27 MB |
| ipc | 48 | 0.22 MB |
| device | 26 | 0.06 MB |
| (جذر المستودع) | 10 | 61.21 MB |

## 3. وثائق التقليم السابقة (موجودة ومقروءة)

- `README.md` — يصف الشجرة كـ «Web-App-Only Rendering Runtime Source».
- `KEEP_ROOTS.md` — 253 جذراً مسموحاً.
- `DOWNLOADS.md` — سجل الاعتماديات المنزّلة كأرشيفات `+archive/<commit>.tar.gz` مع SHA256.
- `NEEDED_DEPS.md` / `CUT_DEPS.md` — تحليل اعتماديات third_party والاعتماديات المقطوعة عمداً.
- `REACHABLE.txt` / `UNREACHABLE.txt` — إغلاق الاعتماديات عبر `#include`/`BUILD.gn`/`DEPS`.
- `REMOVED.txt` — سجل حذف **339,051 ملفاً / 4,134.42 MB** من التقليم السابق.
- `MISSING_INCLUDES.txt` — 1,706 رأساً مقطوعاً عمداً + ملاحظة أن الملفات المولّدة (`*.mojom.h`, `*.pb.h`, `*buildflags.h`) غير موجودة في المصدر الخام.
- `chromium-158.0.8127.89.DEPS` — لقطة DEPS الأصلية (مرجع الإصدارات المثبّتة).

**قاعدة التقليم السابق:** «تنزيل وحذف فقط، دون تعديل أي سطر مصدري». لذلك الشجرة تحتوي اعتماديات مقطوعة موثّقة (غير مترابطة بالكامل) وليست مصدراً قابلاً للبناء كما هي.

## 4. البنية والروابط الرمزية

الشجرة تستخدم روابط رمزية للحفاظ على مسارات `#include` الرسمية رغم نقل المجلدات إلى الجذر:

- `third_party/blink → ../blink`
- `third_party/angle → ../angle`
- `third_party/skia → ../skia`
- `third_party/icu → ../icu`
- `third_party/harfbuzz-ng/src → ../../harfbuzz`
- `components/viz → ../viz`

## 5. حالة منظومة بناء Chromium (قبل) — مطلوبة الإزالة بالكامل

| النوع | العدد |
|---|---:|
| `BUILD.gn` | 763 |
| `*.gni` | 305 |
| `.gn` | 1 |
| `DEPS` | 503 |
| `OWNERS` | 555 |
| `DIR_METADATA` | 302 |
| `PRESUBMIT.py` | 17 |
| مجلد `build/` | 245 ملفاً (معظمه GN/toolchain/scripts) |
| سكربتات تستدعي gn/ninja/gclient/depot_tools | 25 |
| مجلدات مساعدات GN | `skia/gn`, `angle/gni`, `v8/gni`, `third_party/perfetto/gn`, `base/allocator/partition_allocator/gn`, `*/build_overrides` |

**رؤوس مصدرية أساسية داخل `build/` يجب الإبقاء عليها** (ليست أدوات بناء):
- `build/build_config.h` — مضمّن في **2,334** ملفاً.
- `build/buildflag.h` — مضمّن في 55 ملفاً.
- `build/sanitizers/sanitizer_shared_hooks.h` ومصدرها.
- `build/rust/allocator/*.{h,cc,rs}` و`build/rust/chromium_prelude/*.rs` (كود Rust/C++ مصدري).
- ملاحظة: `compiler_specific.h` انتقل upstream إلى `base/compiler_specific.h` وهو موجود.

## 6. المكونات الموجودة فعلياً (تحقق بالملفات لا بالأسماء)

### موجودة وسليمة البنية
- **Blink core**: HTML/DOM/CSS/Style/LayoutNG/Paint/SVG/Forms/Canvas/Events/Editing/Input/Loader/Fetch/XHR/Workers/Scheduler/Script/Streams/FileAPI/URL/Animation/Fullscreen/Clipboard/Messaging/OffscreenCanvas/ResizeObserver/IntersectionObserver/TrustedTypes/MathML/ViewTransition.
- **Blink modules الموجودة**: webgl, webaudio, webcodecs, websockets, webtransport, service_worker, indexeddb, cache_storage, canvas, clipboard, compression, crypto, encryptedmedia, eventsource, file_system_access, filesystem, font_access, keyboard, locks, mediasession, mediasource, netinfo, quota, screen_orientation, storage, virtualkeyboard, window_controls_overlay, worklet, broadcastchannel, beacon, buckets.
- **V8** كاملاً (Ignition/Sparkplug/Maglev/TurboFan/Oilpan/Wasm) — `v8/src`, `v8/include`.
- **Skia** (Ganesh/Graphite/skcms/skshaper/skparagraph/skunicode/svg).
- **ANGLE** (OpenGL ES / WebGL 1/2، ترجمة GLSL).
- **SwiftShader** (رسم برمجي).
- **ICU + HarfBuzz + FreeType** (Unicode/RTL/تشكيل عربي).
- **net** (HTTP/1.1–3, TLS, cookies, cache, websockets, QUIC) — **بدون `net/cert`**.
- **media** (ffmpeg, libvpx, libaom, dav1d, opus, flac, filters, renderers) — **بدون `media/capture` و`media/webrtc`**.
- **gpu** (command_buffer, GLES2, ipc, vulkan) — ملفات `dawn_*` موجودة جزئياً لكن **بدون `webgpu_decoder` ولا `gpu/webgpu`**.
- **cc / viz / mojo / base / sandbox / gin / ipc / url / crypto / sql / storage / dbus**.
- **ui**: gfx, gl, ozone, aura, events, compositor, color, display, latency, platform_window, accessibility, menus, native_theme, shell_dialogs, touch_selection, wm.
- **services**: network, viz, audio, data_decoder, device (جزئي), proxy_resolver, resource_coordinator, service_manager, tracing.
- **components**: webcrypto, viz, services/storage, discardable_memory, memory_pressure, power_monitor, tracing, input, leveldb_proto, sqlite_proto/vfs, os_crypt, surface_embed, metal_util, prefs, performance_manager, وغيرها.
- **content**: renderer, gpu, child, common, utility, renderer_host, worker_host, service_worker, storage hosts, browser (جزئي).

### مفقودة ومطلوبة بالمهمة (ستُستكمل من المصدر الرسمي المطابق)
1. **WebGPU / Dawn** — `third_party/dawn`, `blink/renderer/modules/webgpu`, `gpu/webgpu`, `gpu/command_buffer/{client,common,service}/webgpu*`, `third_party/spirv-tools`, `third_party/spirv-cross`.
2. **WebRTC** — `third_party/webrtc`, `third_party/webrtc_overrides`, `third_party/libsrtp`, `third_party/jsoncpp`, `third_party/crc32c`, `blink/renderer/modules/{peerconnection,mediastream,mediarecorder,mediacapturefromelement,webrtc}`, `blink/renderer/platform/{mediastream,peerconnection}`, `media/webrtc`, `media/capture`.
3. **Geolocation** — `blink/renderer/modules/geolocation`, `services/device/geolocation`, `content/browser/geolocation`, mojom ذات الصلة.
4. **Notifications / Push** — `blink/renderer/modules/{notifications,push_messaging}`, `content/browser/{notifications,push_messaging}`, `components/push_messaging`, mojom ذات الصلة.
5. **Media Capture** — `media/capture`, `blink/renderer/modules/mediastream` (getUserMedia).
6. **التحقق من شهادات TLS** — `net/cert`, `net/cert_net`, بيانات الجذور `net/data/ssl/{chrome_root_store,root_stores,blocklist}` (ضروري لاتصال HTTPS آمن بخادم التطبيق).
7. **Permissions API** — `blink/renderer/modules/permissions` (تحتاجها أذونات الكاميرا/الميكروفون/الإشعارات/الموقع).
8. **mojom واجهات** — `blink/public/mojom/{notifications,push_messaging,mediastream,peerconnection,permissions}` و`services/device/public/{mojom,cpp}` (geolocation).

### ملاحظات فحص
- لا توجد أسرار/مفاتيح حقيقية؛ نتائج الفحص اقتصرت على شهادات اختبار عامة في `net/third_party/quiche` (بيانات اختبار علنية).
- `blink/web_tests` و`blink/perf_tests` المتبقية هي **ملفات تراخيص فقط** (50 ملفاً) — تُحفظ بموجب شرط عدم حذف التراخيص.
- `v8/test` المتبقي (52KB) اختبارات أساسية صغيرة — تُحفظ.
- لا توجد ملفات تنفيذية أو مخرجات بناء.
- لا توجد مكونات مكررة فعلية؛ الروابط الرمزية تمنع الازدواج (مثل `third_party/skia → skia`).

## 7. تعارضات التقليم السابق مع متطلبات المهمة الحالية

التقليم السابق أزال عمدًا (الفئة 8.5) مكونات **تطلبها المهمة الحالية صراحةً**: WebGPU/Dawn، WebRTC، Geolocation، Notifications/Push، Media Capture، والتحقق من الشهادات. لذلك تشمل هذه المهمة **استعادتها** من المصدر الرسمي عند نفس الإصدار المثبّت، مع الحفاظ على قاعدة «عدم استخراج مكونات المتصفح غير المطلوبة».

## 8. خطة التنفيذ المعتمدة

1. إزالة منظومة بناء Chromium بالكامل (GN/Ninja/GYP/gclient/depot_tools/autoninja + البنية التحتية للمشروع) مع الإبقاء على الرؤوس المصدرية الضرورية داخل `build/`.
2. استعادة المكونات الناقصة أعلاه من المصدر الرسمي المطابق (Chromium `1de57fa1…`, Dawn `6e245424…`, WebRTC `fb1c41a9…` والمكتبات المثبّتة في DEPS).
3. تنظيف بقايا واجهة المتصفح غير الضرورية بعد فحص الاعتماديات.
4. فحوص مصدرية ساكنة (بدون أي Build/Compile).
5. توثيق شامل (9 وثائق) + Commit + Push إلى `main` بدون Force.

---

# بعد التعديل — النتائج الفعلية

## 9. المقاييس بعد التعديل

| المقياس | قبل | بعد |
|---|---:|---:|
| الملفات (عادية + روابط) | 59,545 | **~71,450** |
| حجم شجرة العمل | 849.59 MB | **~963 MB** |
| ملفات التراخيص | 313 | **335** (لم يُحذف أي ترخيص؛ أُضيفت تراخيص المستعاد + أُعيد ترخيص libxslt) |
| منظومة بناء Chromium | موجودة (2,963 ملفاً) | **مُزالة بالكامل (0)** |
| WebGPU / Dawn | مفقود | **مستكمل** |
| WebRTC / Media Capture | مفقود | **مستكمل** |
| Geolocation / Notifications / Push / Permissions | مفقودة | **مستكملة** |
| التحقق من TLS (net/cert + BoringSSL pki) | مفقود | **مستكمل** |

- **أُضيف:** ~16,750 ملفاً (~140 MB) من المصادر الرسمية المطابقة.
- **أُزيل:** 4,884 ملفاً + 10 روابط رمزية مكسورة (منها 2,963 لمنظومة البناء، و1,911 تنظيف اختبارات/fuzzers/أجزاء ML اختيارية).

## 10. الفحص الساكن النهائي للاعتماديات (`#include`)

| التصنيف | التكرارات | الفريد |
|---|---:|---:|
| محلول | 342,227 | — |
| مولّد وقت البناء (طبيعي الغياب) | 14,071 | 3,612 |
| أطر اختبار (gtest/gmock غير مضمّنة) | 440 | 129 |
| منصات محذوفة (Android/iOS/ChromeOS/Fuchsia) | 627 | 174 |
| قطوع متعمدة (DevTools/ميزات متصفح) | 967 | 349 |
| نقص متبقٍ (ذيل اختياري) | 1,567 | 1,245 |

**الخلاصة:** الاعتماديات المصدرية الأساسية للمكونات المستعادة (WebGPU/WebRTC/cert/permissions…) **محلولة**. المتبقي رؤوس مولّدة (ينتجها البناء المستقبلي)، أطر اختبار، منصات محذوفة، قطوع متعمدة موثّقة، وذيل اختياري صغير (أجزاء tflite/opus/subzero/clspv). التفاصيل في [`MISSING_COMPONENTS.md`](MISSING_COMPONENTS.md) و[`DEPENDENCY_MAP.md`](DEPENDENCY_MAP.md).

## 11. تحقق المكونات الحرجة (موجودة بعد التعديل)

`third_party/dawn/src/{dawn,tint}` ✅ · `third_party/webrtc/{pc,modules}` ✅ · `blink/renderer/modules/webgpu` ✅ · `blink/renderer/modules/peerconnection` ✅ · `blink/renderer/core/geolocation` ✅ · `blink/renderer/modules/notifications` ✅ · `net/cert` ✅ · `gpu/webgpu` ✅ · `media/capture` ✅ · `v8/src/wasm` ✅ · `skia/src/gpu/graphite/dawn` ✅ · `angle/src/libANGLE` ✅ · الروابط الرمزية الحرجة سليمة ✅ · لا أسرار/مفاتيح ✅ · لا ملفات تنفيذية/مخرجات بناء ✅.

## 12. الوثائق الناتجة

[`COMPONENT_INVENTORY.md`](COMPONENT_INVENTORY.md) · [`DEPENDENCY_MAP.md`](DEPENDENCY_MAP.md) · [`REMOVED_FILES.md`](REMOVED_FILES.md) · [`MISSING_COMPONENTS.md`](MISSING_COMPONENTS.md) · [`RUNTIME_ARCHITECTURE.md`](RUNTIME_ARCHITECTURE.md) · [`WEB_PLATFORM_SUPPORT.md`](WEB_PLATFORM_SUPPORT.md) · [`BUILD_SYSTEM_REMOVAL.md`](BUILD_SYSTEM_REMOVAL.md) · [`THIRD_PARTY_LICENSES.md`](THIRD_PARTY_LICENSES.md) · السجلات الخام في [`docs/logs/`](docs/logs/).

> **لم يُنفّذ أي Build أو Compile، ولم يُنشأ نظام بناء بديل، ولم تُنتج ملفات تنفيذية.** التوافق التشغيلي مع أطر الويب غير متحقق (يتطلب مرحلة بناء مستقبلية)؛ ما تم إثباته هو وجود البنية المصدرية والاعتماديات ساكنياً.
