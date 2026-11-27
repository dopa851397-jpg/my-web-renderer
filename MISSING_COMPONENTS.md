# MISSING_COMPONENTS.md — المكونات الناقصة وكيفية استكمالها والمتبقي

> الإصدار المرجعي: Chromium `1de57fa19722fa6d6841d4f596c394d015580656` (158.0.8127.89). جميع الاستعادات من مصادر رسمية مطابقة (Chromium/V8/Skia/ANGLE/Dawn/WebRTC/BoringSSL/Khronos/TensorFlow). السجلات: `docs/logs/fetch_manifest*.json` (روابط + SHA256).

## أ. مكونات كانت مفقودة وأُكملت بالكامل

| المكون | كان مفقوداً لأن | المصدر | الحالة |
|---|---|---|---|
| **WebGPU / Dawn / Tint** | التقليم السابق منعه (8.5) | Dawn `6e245424` + Chromium src | ✅ مكتمل مصدرياً |
| **WebRTC** | التقليم السابق منعه (8.5) | WebRTC `fb1c41a9` + Chromium src | ✅ مكتمل مصدرياً |
| **Media Capture** | حُذف مع WebRTC | Chromium src `media/capture`, `modules/mediastream` | ✅ مكتمل |
| **Geolocation** | حُذف (8.5)؛ نُقل إلى core في 158 | Chromium src `core/geolocation`, `services/device/geolocation` | ✅ مكتمل |
| **Notifications / Push** | حُذف (8.5) | Chromium src | ✅ واجهات + content؛ backend للـ Embedder |
| **Permissions API** | حُذف | Chromium src `modules/permissions`, `content/browser/permissions` | ✅ مكتمل |
| **التحقق من TLS (net/cert + BoringSSL pki)** | حُذف (8.2) | Chromium src + BoringSSL `ea9f3a34` | ✅ مكتمل (ضروري لـ HTTPS) |
| **SPIRV-Tools / SPIRV-Cross / استكمال SPIRV-Headers** | غير مضمّنة | Khronos pinned | ✅ مكتمل |
| **خلفية Skia Graphite/Dawn** | حُذفت مع WebGPU | Skia `3279352f` | ✅ مكتمل |
| **libsrtp / jsoncpp / crc32c / sframe** | غير مضمّنة | pinned DEPS | ✅ مكتمل |
| **base/metrics / services/metrics public / cc/metrics** | حُذفت (8.2 tracking) | Chromium src | ✅ أُعيدت كبنية تحتية مشتركة (لا تقارير متصفح) |
| **net/proxy_resolution / net/reporting / net/storage_access_api** | حُذفت | Chromium src | ✅ مكتمل |
| **components/{webrtc,push_messaging,crash/core/common}** | حُذفت | Chromium src | ✅ مكتمل |
| **media/cdm + api** | حُذف | Chromium src + chromium/cdm `d6c4e1ea` | ✅ مكتمل |
| **origin_trials / media_session cpp / platform/{p2p,webrtc,video_capture}** | حُذفت | Chromium src | ✅ مكتمل |

## ب. تحسينات ML الصوتية الاختيارية (WebRTC) — مضمّنة جزئياً

| المكون | الحالة | ملاحظة |
|---|---|---|
| tflite-lite (نواة المفسّر) | مضمّن جزئياً | أُضيفت النواة + core/platform + core/lib + mlir/lite core. الأجزاء التجريبية (genai/microfrontend) والوفود الثقيلة (xnnpack/ynnpack/hexagon/gpu) وأدوات التطوير **أُزيلت** لأنها لا تُترجم في Chromium لصوتيات WebRTC. |
| farmhash / flatbuffers / gemmlowp / ruy | مضمّن | اعتماديات tflite المثبّتة |
| neural_residual_echo_estimator (الواجهة + aec3) | مضمّن | الواجهة المجردة + feature extractor؛ المنشئ المعتمد على tflite موجود عبر media/webrtc |
| **rnn_vad (pffft/rnnoise)** | **أُزيل** | معطّل في Chromium (pffft/rnnoise غير موجودتين في DEPS)؛ أُزيل بالاتساق مع Chromium. AEC3/AGC2/NS القياسية كاملة. |

> **الصدق:** مسار تقدير الصدى العصبي/عزل الصوت يعتمد على شجرة tflite/MLIR كاملة؛ النواة المضمّنة تغطي الاستخدام الأساسي لكن بعض نوى tflite الاختيارية (pybind11/parse_example/hashtable) غير مضمّنة. **WebRTC القياسي (AEC3/AGC2/NS + كل مسارات الصوت/الفيديو/البيانات) مكتمل ولا يعتمد على هذه الأجزاء الاختيارية.**

## ج. نواقص متبقية موثّقة (غير مانعة لتشغيل تطبيقات الويب)

هذه فئات متبقية من الفحص الساكن (1,567 تكراراً / 1,245 فريداً)، معظمها **ليس نقصاً مصدر أساسياً**:

1. **رؤوس مولّدة وقت البناء (14,071 تكراراً):** `*.mojom.h`, `*.pb.h`, `*buildflags.h`, bindings V8، CSS/HTML names، Perfetto pbzero، X11 protocol. **طبيعية الغياب في المصدر الخام**؛ ينتجها نظام البناء/codegen المستقبلي. بيانات المصدر (.mojom/.idl/.json5/.proto) محفوظة.
2. **أطر اختبار (440):** gtest/gmock غير مضمّنة (الاختبارات ليست مطلوبة للتشغيل).
3. **منصات محذوفة (627):** Android/iOS/ChromeOS/Fuchsia — منصات غير مدعومة عن قصد.
4. **قطوع متعمدة (967):** DevTools/Inspector، ميزات متصفح (back_forward_cache, web_package, download, autofill, payments, safe_browsing, ad_tracker, variations…) — موثّقة في `CUT_DEPS.md`. لا تحتاجها تطبيقات الويب الأساسية.
5. **ذيل اختياري صغير:** أجزاء tflite الاختيارية (أعلاه)، opus lpcnet/dsplib (ترميز عصبي/DSP اختياري)، SwiftShader Subzero (مترجم بديل؛ LLVM Reactor هو الافتراضي)، ANGLE clspv (backend OpenCL اختياري)، `ui/gfx/x/extension_manager.h` (X11 ثانوي)، `TargetConditionals.h` (رأس Apple نظامي).

## د. فجوات معمارية للـ Embedder المستقبلي (ليست نقصاً في هذا المصدر)

- **طبقة Embedder** (`ContentMainDelegate`, `ContentBrowserClient`, `ContentRendererClient`): كانت في `chrome/` المحذوف؛ يكتبها Ultra Desktop Framework.
- **نظام بناء + codegen مستقل**: أُزيلت منظومة Chromium؛ الـ Embedder يوفّرها.
- **Push backend / CDM فعلي**: الواجهات موجودة؛ التوصيل الفعلي للـ Embedder.
- **DevTools**: محذوف؛ يمكن إعادة جلبه اختيارياً.
- **libxslt/XSLT**: المصدر مقلم من خط الأساس (بقيت config + الترخيص)؛ ميزة ويب قديمة اختيارية.

## هـ. كيفية إعادة الاستكمال مستقبلاً

كل استعادة موثّقة في `docs/logs/fetch_manifest*.json` بالرابط والـ commit وSHA256. لأي مكون ناقص: استخدم `https://chromium.googlesource.com/chromium/src/+archive/<commit>/<path>.tar.gz` عند نفس الإصدار المثبّت، أو المستودع الخارجي المقابل من `docs/provenance/chromium-158.0.8127.89.DEPS.txt`.
