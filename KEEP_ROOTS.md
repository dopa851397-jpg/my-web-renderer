# KEEP_ROOTS.md — الجذور الوحيدة المسموحة لبيئة تشغيل تطبيقات الويب (Chromium 158.0.8127.89)

تحدد هذه الوثيقة الجذور الوحيدة المسموحة لمصدر **عرض تطبيقات الويب المبنية فقط**؛ كل ما عداها يُحذف ما لم يكن لازماً لها عبر إغلاق الاعتماديات (`#include` / `BUILD.gn` / `DEPS`) بشرط ألا يقع ضمن القوائم الممنوعة في الخطوة 8.

- **إجمالي المسارات الجذرية المعتمدة:** 253 مساراً (تم التحقق برمجياً من وجودها جميعاً على القرص).

## أ. Blink (HTML/DOM/CSS/Style/Layout/Paint، bindings، scheduler، workers، fetch، storage، forms، canvas، events، SVG، text/fonts)

| المسار الجذري | الوظيفة وسبب الإبقاء |
|---|---|
| `blink/renderer/core/html` | تحليل HTML وعناصر الـ DOM والنماذج (forms) و`<canvas>` و`<audio>`/`<video>` |
| `blink/renderer/core/dom` | شجرة DOM الأساسية والعقد والأحداث والمراقبات |
| `blink/renderer/core/css` | محلل CSS وقواعد المطابقة والمتغيرات والاستعلامات |
| `blink/renderer/core/style` | تمثيل الأنماط المحسوبة (ComputedStyle) |
| `blink/renderer/core/layout` | محرك التخطيط LayoutNG (بما فيه الجداول وFlex/Grid وRTL) |
| `blink/renderer/core/paint` | تحويل شجرة التخطيط إلى أوامر رسم |
| `blink/renderer/core/svg` | عناصر ورسوميات SVG |
| `blink/renderer/core/events` | نظام أحداث DOM والمؤشر ولوحة المفاتيح |
| `blink/renderer/core/editing` | تحرير النصوص، التحديد، والمؤشر النصي داخل النماذج |
| `blink/renderer/core/input` | معالجة أحداث الفأرة واللمس ولوحة المفاتيح والتمرير |
| `blink/renderer/core/frame` | الإطار المحلي `LocalFrame` ونافذة `DOMWindow` |
| `blink/renderer/core/page` | إدارة الصفحة والتركيز ودورة حياة العرض |
| `blink/renderer/core/loader` | تحميل موارد التطبيق (HTML/CSS/JS/Fonts/Images) |
| `blink/renderer/core/fetch` | واجهة `fetch()` و`Request`/`Response`/`Headers` |
| `blink/renderer/core/xmlhttprequest` | واجهة `XMLHttpRequest` |
| `blink/renderer/core/workers` | البنية الأساسية لـ Web Workers (`Worker`, `SharedWorker`, `Worklet`) |
| `blink/renderer/core/scheduler` | مجدول مهام Blink والأولويات |
| `blink/renderer/core/script` | تحميل وتنفيذ السكربتات الكلاسيكية ووحدات ES Modules |
| `blink/renderer/core/execution_context` | سياق التنفيذ المشترك بين النافذة والـ Workers |
| `blink/renderer/core/streams` | واجهات `ReadableStream` و`WritableStream` و`TransformStream` |
| `blink/renderer/core/fileapi` | واجهات `Blob` و`File` و`FileReader` |
| `blink/renderer/core/typed_arrays` | مصفوفات البايت الثنائية لمبادلة البيانات مع V8/WebGL/WebAudio |
| `blink/renderer/core/url` | واجهات `URL` و`URLSearchParams` |
| `blink/renderer/core/url_pattern` | واجهة `URLPattern` لتوجيه المسارات داخل التطبيق |
| `blink/renderer/core/xml` | تحليل XML و`DOMParser` و`XMLSerializer` |
| `blink/renderer/core/animation` | محرك التحريك Web Animations وCSS Animations/Transitions |
| `blink/renderer/core/animation_frame` | واجهة `requestAnimationFrame` |
| `blink/renderer/core/geometry` | `DOMRect` و`DOMMatrix` و`DOMPoint` |
| `blink/renderer/core/scroll` | البنية الأساسية للتمرير |
| `blink/renderer/core/overscroll` | سلوك حدود التمرير |
| `blink/renderer/core/resize_observer` | واجهة `ResizeObserver` |
| `blink/renderer/core/intersection_observer` | واجهة `IntersectionObserver` |
| `blink/renderer/core/view_transition` | انتقالات العرض داخل التطبيق `ViewTransition` |
| `blink/renderer/core/display_lock` | `content-visibility` لتحسين أداء التخطيط |
| `blink/renderer/core/fullscreen` | وضع ملء الشاشة لتطبيقات الويب |
| `blink/renderer/core/clipboard` | أحداث الحافظة الأساسية |
| `blink/renderer/core/messaging` | `MessageChannel` و`MessagePort` و`postMessage` |
| `blink/renderer/core/mojo` | جسور Mojo الداخلية في Blink |
| `blink/renderer/core/offscreencanvas` | `OffscreenCanvas` للرسم من داخل الـ Workers |
| `blink/renderer/core/imagebitmap` | `ImageBitmap` و`createImageBitmap` |
| `blink/renderer/core/timing` | واجهات `Performance` وقياس التوقيت |
| `blink/renderer/core/timezone` | مراقبة المنطقة الزمنية |
| `blink/renderer/core/trustedtypes` | سياسات أمان DOM (`TrustedTypes`) |
| `blink/renderer/core/sanitizer` | تنقية HTML الآمنة |
| `blink/renderer/core/highlight` | واجهة تمييز النصوص البرمجية CSS Custom Highlight |
| `blink/renderer/core/mathml` | عرض المعادلات الرياضية MathML |
| `blink/renderer/core/context_features` | تفعيل ميزات السياق |
| `blink/renderer/core/exported` | الواجهة المُصدَّرة لربط Blink مع `content/renderer` |
| `blink/renderer/core/inspector/console_message.h` | نقطة تسجيل أخطاء بسيطة مسموحة صراحةً (الخطوة 8) دون DevTools |
| `blink/renderer/core/inspector/console_message.cc` | تنفيذ رسالة تسجيل الأخطاء البسيطة |
| `blink/renderer/core/inspector/console_message_storage.h` | تخزين رسائل الأخطاء البسيطة |
| `blink/renderer/core/inspector/console_message_storage.cc` | تنفيذ تخزين رسائل الأخطاء البسيطة |
| `blink/renderer/bindings` | ربط V8 بكائنات DOM وواجهات الويب |
| `blink/renderer/controller` | تهيئة وتشغيل Blink داخل عملية الـ renderer |
| `blink/renderer/platform/fonts` | محرك الخطوط وتشكيل الحروف مع HarfBuzz وFreeType |
| `blink/renderer/platform/text` | خوارزميات Unicode ثنائية الاتجاه (BiDi / RTL) والعربية مع ICU |
| `blink/renderer/platform/graphics` | طبقة التجريد الرسومي فوق Skia وcc وgpu |
| `blink/renderer/platform/audio` | نواة معالجة الإشارات الصوتية لـ WebAudio |
| `blink/renderer/platform/media` | تكييف مشغلات الصوت والفيديو داخل الـ renderer |
| `blink/renderer/platform/media_capabilities` | بيانات قدرات الوسائط |
| `blink/renderer/platform/image-decoders` | فك ترميز الصور (PNG, JPEG, WebP, AVIF, GIF, BMP, ICO) |
| `blink/renderer/platform/image-encoders` | ترميز الصور لـ `canvas.toBlob` / `toDataURL` |
| `blink/renderer/platform/loader` | جلب الموارد على مستوى المنصة لـ `fetch` والسكربتات |
| `blink/renderer/platform/network` | رؤوس وحالات HTTP وWebSocket على مستوى Blink |
| `blink/renderer/platform/blob` | إدارة كائنات `Blob` |
| `blink/renderer/platform/storage` | مفاتيح التخزين المعزولة للتطبيق (`BlinkStorageKey`) |
| `blink/renderer/platform/scheduler` | مجدول خيوط الـ renderer والـ workers |
| `blink/renderer/platform/bindings` | البنية التحتية لربط V8 وإدارة الأغلفة |
| `blink/renderer/platform/heap` | جامع القمامة Oilpan لكائنات Blink |
| `blink/renderer/platform/wtf` | حاويات وسلاسل وأدوات Blink الأساسية |
| `blink/renderer/platform/weborigin` | تمثيل `SecurityOrigin` وسياسة المصدر |
| `blink/renderer/platform/widget` | ربط إطار العرض بالـ compositor ومدخلات النافذة |
| `blink/renderer/platform/geometry` | الأنواع الهندسية الأساسية لـ Blink |
| `blink/renderer/platform/transforms` | مصفوفات التحويل الثنائية والثلاثية الأبعاد |
| `blink/renderer/platform/animation` | منحنيات التوقيت والتحريك |
| `blink/renderer/platform/json` | محلل ومُنشئ JSON الداخلي |
| `blink/renderer/platform/mojo` | أدوات ربط Mojo في منصة Blink |
| `blink/renderer/platform/theme` | سمات عناصر النماذج الافتراضية |
| `blink/renderer/platform/cpu` | اكتشاف ميزات المعالج SIMD |
| `blink/renderer/platform/instrumentation` | عدادات الذاكرة والأداء الأساسية |
| `blink/renderer/platform/exported` | الواجهات المُصدَّرة لمنصة Blink |
| `blink/public/common` | التعريفات المشتركة بين Blink و`content` |
| `blink/public/mojom` | واجهات Mojo القياسية للميزات المسموحة |
| `blink/public/platform` | واجهات منصة Blink العامة |
| `blink/public/web` | واجهة تضمين Blink العامة |
| `blink/common` | التنفيذات المشتركة لهياكل رسائل Blink |

## ب. V8 كامل (JavaScript و WebAssembly)

| المسار الجذري | الوظيفة وسبب الإبقاء |
|---|---|
| `v8/include` | الواجهات العامة لمحرك V8 |
| `v8/src` | كامل محرك V8 (المحلل، Ignition، Sparkplug، Maglev، TurboFan، جامع القمامة، وWebAssembly `v8/src/wasm`) |
| `v8/third_party/wasm-api` | واجهة WebAssembly C/C++ القياسية |
| `v8/third_party/rapidhash-v8` | التجزئة السريعة داخل V8 |
| `v8/third_party/siphash` | تجزئة SipHash داخل V8 |
| `v8/third_party/utf8-decoder` | فك ترميز UTF-8 داخل V8 |
| `v8/third_party/v8` | ملفات توليد الكود المضمنة في V8 |

## ج. الرسم (skia و cc و viz و gpu و angle برمجي + GL مع WebGL)

| المسار الجذري | الوظيفة وسبب الإبقاء |
|---|---|
| `skia/include` | واجهات Skia العامة للرسم الثنائي الأبعاد وGanesh/Graphite |
| `skia/src` | التنفيذ الكامل لمحرك الرسم Skia (برمجي + GPU GL/Vulkan) |
| `skia/modules/skcms` | إدارة الفضاءات اللونية ICC |
| `skia/modules/skparagraph` | تخطيط الفقرات متعددة اللغات |
| `skia/modules/skshaper` | ربط Skia مع HarfBuzz لتشكيل النصوص |
| `skia/modules/skunicode` | ربط Skia مع ICU لمعالجة Unicode وRTL |
| `skia/modules/svg` | دعم رسم مسارات وعناصر SVG في Skia |
| `skia/ext` | طبقة تكامل Skia مع Chromium |
| `skia/public` | سمات التبادل الرسومي عبر Mojo |
| `skia/config` | إعدادات بناء Skia ضمن المحرك |
| `cc` | مركّب الطبقات (Compositor) وتقسيم البلاطات والتحريك المسرّع |
| `viz/client` | عميل مركّب العرض |
| `viz/common` | هياكل الإطارات المركّبة (`CompositorFrame`, `Quad`) |
| `viz/host` | مضيف خدمة العرض الرسومي |
| `viz/service` | خدمة تركيب الأسطح والعرض (`DisplayCompositor`) |
| `gpu/command_buffer` | مخزن الأوامر الرسومية لعميل وخدمة GPU وWebGL |
| `gpu/config` | معلومات وقدرات معالج الرسوميات |
| `gpu/ipc` | نقل أوامر GPU بين عمليتي renderer وgpu |
| `gpu/GLES2` | تعريفات وامتدادات OpenGL ES 2/3 لـ WebGL |
| `gpu/gpu_export.h` | تصدير رموز طبقة GPU |
| `gpu/gpu_gles2_export.h` | تصدير رموز GLES2 |
| `gpu/gpu_util_export.h` | تصدير أدوات GPU |
| `gpu/raster_export.h` | تصدير واجهة التصيير المسرّع |
| `gpu/vulkan` | طبقة دعم Vulkan الاختيارية للرسم |
| `angle/include` | رؤوس EGL / GLES2 / GLES3 / WebGL القياسية |
| `angle/src/common` | الأدوات المشتركة في ANGLE |
| `angle/src/compiler` | مترجم مظللات WebGL / ESSlang |
| `angle/src/gpu_info_util` | اكتشاف خصائص البطاقة الرسومية في ANGLE |
| `angle/src/image_util` | معالجة صيغ الأنسجة والصور في ANGLE |
| `angle/src/libANGLE` | نواة تنفيذ OpenGL ES وWebGL (الخلفيات البرمجية وGL) |
| `angle/src/libEGL` | واجهة إدارة أسطح وسياقات EGL |
| `angle/src/libGLESv2` | نقاط دخول OpenGL ES 2.0/3.0 وWebGL 1/2 |
| `third_party/swiftshader/include` | واجهات المصيّر البرمجي لـ OpenGL ES / WebGL |
| `third_party/swiftshader/src` | التنفيذ البرمجي لـ GL/Vulkan لعمل ANGLE بدون عتاد رسومي |

## د. النصوص (harfbuzz و icu مع العربية و RTL)

| المسار الجذري | الوظيفة وسبب الإبقاء |
|---|---|
| `harfbuzz/src` | محرك تشكيل الحروف OpenType الكامل (بما فيه العربية `hb-ot-shaper-arabic` وRTL) |
| `third_party/harfbuzz` | ملفات الربط لـ HarfBuzz |
| `icu/source/common` | نواة Unicode وخوارزمية الاتجاه الثنائي UBiDi (العربية وRTL) وتقسيم الكلمات والأسطر |
| `icu/source/i18n` | التدويل والترتيب الأبجدي والتقويمات والأرقام العربية |
| `icu/source/stubdata` | نقطة ربط بيانات `icudtl` |
| `icu/source/data` | جداول بيانات Unicode واللغات (بما فيها العربية `ar` وقواعد RTL) |
| `icu/common` | رؤوس التكيف مع ICU |

## هـ. الأساس (base و url و mojo و services اللازمة و content لربط renderer/gpu فقط)

| المسار الجذري | الوظيفة وسبب الإبقاء |
|---|---|
| `base` | الخيوط، حلقات الرسائل، الذاكرة (`PartitionAlloc`)، الملفات، التوقيت، وتسجيل الأخطاء |
| `url` | تحليل وتطبيع عناوين URL والمخططات المخصصة مثل `app://` |
| `mojo/core` | نواة الاتصال السريع بين العمليات |
| `mojo/public` | واجهات ومكتبات ربط Mojo C/C++/JS |
| `services/network/cors` | التحقق من CORS لطلبات `fetch` وXHR |
| `services/network/disk_cache` | تخزين الكاش الشبكي |
| `services/network/public` | واجهات `URLLoader` و`WebSocket` العامة |
| `services/network/resource_scheduler` | جدولة الطلبات الشبكية |
| `services/network/shared_dictionary` | قواميس الضغط المشتركة |
| `services/network/throttling` | تنظيم تدفق الشبكة |
| `services/viz` | واجهات خدمة العرض الرسومي |
| `services/audio` | خدمة إخراج ومعالجة الصوت لـ WebAudio وMedia |
| `services/data_decoder` | فك ترميز البيانات والصور بأمان في عملية معزولة |
| `services/service_manager/public` | واجهات ربط الخدمات الأساسية |
| `services/resource_coordinator/public` | إشارات تنسيق الذاكرة |
| `services/tracing/public` | نقطة التتبع الأساسية |
| `components/services/storage` | خدمة التخزين الموحدة لـ IndexedDB وCache Storage وlocalStorage |
| `components/services/font` | خدمة توفير الخطوط لعملية الـ renderer |
| `components/services/font_data` | نقل بيانات الخطوط للـ renderer |
| `components/services/filesystem` | واجهة الملفات المعزولة للتخزين |
| `content/renderer` | عملية الـ Renderer التي تستضيف Blink وV8 |
| `content/gpu` | عملية الـ GPU التي تستضيف Viz وANGLE وSkia |
| `content/child` | البنية المشتركة للعمليات الفرعية (renderer/gpu/utility) |
| `content/common` | رسائل وهياكل الربط بين العمليات |
| `content/app` | نقطة تشغيل وتهيئة عمليات المحرك |
| `content/utility` | عملية استضافة الخدمات المساندة (الصوت/الشبكة/التخزين) |
| `content/zygote` | تمهيد العمليات المعزولة على Linux |
| `content/public/app` | واجهة بدء تشغيل بيئة التشغيل |
| `content/public/child` | واجهة العمليات الفرعية العامة |
| `content/public/common` | الإعدادات والمفاتيح المشتركة (بما فيها تسجيل البروتوكولات المخصصة `app://`) |
| `content/public/gpu` | واجهة تهيئة GPU العامة |
| `content/public/renderer` | واجهة تخصيص الـ renderer العامة |
| `content/public/utility` | واجهة عملية الخدمات العامة |
| `content/browser/gpu` | مضيف قناة GPU وربطها بالـ renderer |
| `content/browser/compositor` | ربط سطح العرض المركّب بعملية GPU |
| `content/browser/renderer_host` | مضيف عملية الـ renderer وتمرير المدخلات والإطارات الرسومية |
| `content/browser/worker_host` | مضيف Dedicated Workers وShared Workers |
| `content/browser/service_worker` | مضيف دورة حياة Service Workers |
| `content/browser/service_host` | تشغيل خدمات الشبكة والصوت والتخزين |
| `content/browser/indexed_db` | تنسيق مضيف IndexedDB |
| `content/browser/cache_storage` | تنسيق مضيف Cache Storage |
| `content/browser/dom_storage` | مضيف `localStorage` و`sessionStorage` |
| `content/browser/blob_storage` | مضيف تخزين `Blob` |
| `content/browser/buckets` | مضيف Storage Buckets |
| `content/browser/quota` | إدارة حصص التخزين المحلي للتطبيق |
| `content/browser/file_system` | دعم نظام الملفات المعزول للتطبيق |
| `content/browser/locks` | مضيف Web Locks API |
| `content/browser/code_cache` | تخزين بايت-كود V8 وWASM المترجم لتسريع إقلاع التطبيق |
| `content/browser/broadcast_channel` | مضيف `BroadcastChannel` بين الـ workers والإطارات |
| `content/browser/websockets` | ربط اتصالات WebSocket بخدمة الشبكة |
| `content/browser/loader` | ربط محمّل الموارد (`URLLoaderFactory`) بما فيه معالجات `app://` المحلية |
| `content/browser/network` | ربط عملية الـ renderer بخدمة الشبكة |
| `content/browser/media` | ربط أنابيب الصوت والفيديو بعمليتي GPU والصوت |
| `content/browser/audio` | ربط تدفقات WebAudio بخدمة الصوت |
| `content/browser/font_unique_name_lookup` | مطابقة أسماء الخطوط المحلية |
| `content/browser/scheduler` | مجدول خيوط الربط الأساسية |
| `content/browser/zygote_host` | إدارة عمليات Zygote على Linux |

## و. الشبكة `net` (فقط ما يلزم لـ fetch و XHR و WebSocket لاتصال التطبيق بخادمه، وتحميل `app://` المحلي)

| المسار الجذري | الوظيفة وسبب الإبقاء |
|---|---|
| `net/base` | الأنواع الشبكية، أنواع MIME، وتدفقات الملفات المحلية (`FileStream`) لتحميل أصول `app://` |
| `net/http` | معاملات واتصالات ورؤوس وكاش HTTP/1.1 لـ `fetch` وXHR |
| `net/websockets` | بروتوكول وإطارات ومصافحة `WebSocket` (`ws://` و`wss://`) |
| `net/url_request` | إدارة الطلبات ووظائف المخططات المخصصة (`URLRequestJob` لبناء محمّل `app://`) |
| `net/socket` | مقابس TCP وTLS لنقل طلبات الخادم وWebSocket |
| `net/ssl` | إعدادات وجلسات TLS للاتصال الآمن بخادم التطبيق |
| `net/spdy` | بروتوكول HTTP/2 لتسريع طلبات `fetch` المتزامنة |
| `net/quic` | بروتوكول HTTP/3 / QUIC لاتصال التطبيق بخادمه |
| `net/dns` | حل أسماء النطاقات لخادم التطبيق |
| `net/cookies` | تخزين وإرسال الكوكيز الخاصة بجلسة خادم التطبيق |
| `net/disk_cache` | تخزين استجابات الخادم محلياً |
| `net/filter` | فك ضغط تدفقات الاستجابة (Gzip / Brotli / Zstd) |
| `net/shared_dictionary` | فك الضغط بالقواميس المشتركة |
| `net/log` | بنية السجلات التشخيصية الخفيفة المطلوبة داخلياً لمقابس الشبكة |
| `net/traffic_annotation` | تعريفات الوسوم المطلوبة لتوقيعات دوال `net` |
| `net/third_party/quiche` | تنفيذ إطارات HTTP/2 وHTTP/3 وWebSocket المشتركة |
| `net/third_party/uri_template` | توسيع قوالب العناوين القياسية |

## ز. الميزات (WebGL، Canvas، WebAudio، Media، Workers، Service Workers، IndexedDB، WebSocket، WebAssembly)

| المسار الجذري | الوظيفة وسبب الإبقاء |
|---|---|
| `blink/renderer/modules/webgl` | واجهة WebGL 1.0 وWebGL 2.0 الكاملة |
| `blink/renderer/modules/canvas` | واجهة Canvas 2D وOffscreenCanvas وImageBitmapRenderingContext |
| `blink/renderer/modules/webaudio` | واجهة WebAudio الكاملة (`AudioContext`, `AudioWorklet`, العقد الصوتية) |
| `blink/renderer/modules/media` | ضوابط وتكامل عناصر الوسائط |
| `blink/renderer/modules/mediasource` | واجهة `MediaSource Extensions (MSE)` لبث الفيديو والصوت |
| `blink/renderer/modules/media_capabilities` | واجهة `MediaCapabilities` |
| `blink/renderer/modules/media_controls` | عناصر التحكم الأساسية لمشغل الوسائط |
| `blink/renderer/modules/webcodecs` | واجهة `WebCodecs` لفك وترميز الصوت والفيديو المسرّع |
| `blink/renderer/modules/video_rvfc` | `requestVideoFrameCallback` لمزامنة الفيديو مع Canvas/WebGL |
| `blink/renderer/modules/srcobject` | ربط مصادر الوسائط بعناصر العرض |
| `blink/renderer/modules/service_worker` | واجهة Service Workers للتخزين والعمل دون اتصال |
| `blink/renderer/modules/worklet` | بنية Worklets الصوتية والرسومية |
| `blink/renderer/modules/animationworklet` | تحريك الرسوميات في خيط مستقل |
| `blink/renderer/modules/csspaint` | واجهة CSS Painting API (Houdini) |
| `blink/renderer/modules/indexeddb` | قاعدة بيانات `IndexedDB` الكاملة داخل التطبيق |
| `blink/renderer/modules/cache_storage` | واجهة `Cache` و`CacheStorage` لأصول التطبيق |
| `blink/renderer/modules/storage` | واجهتا `localStorage` و`sessionStorage` |
| `blink/renderer/modules/buckets` | واجهة Storage Buckets |
| `blink/renderer/modules/quota` | واجهة `navigator.storage` |
| `blink/renderer/modules/filesystem` | نظام الملفات المحلي المعزول (OPFS) |
| `blink/renderer/modules/locks` | تنسيق الوصول المتزامن عبر `navigator.locks` |
| `blink/renderer/modules/websockets` | واجهة `WebSocket` و`WebSocketStream` في JS |
| `blink/renderer/modules/eventsource` | واجهة `EventSource` (Server-Sent Events) |
| `blink/renderer/modules/broadcastchannel` | واجهة `BroadcastChannel` |
| `blink/renderer/modules/encoding` | `TextEncoder` و`TextDecoder` |
| `blink/renderer/modules/compression` | `CompressionStream` و`DecompressionStream` |
| `blink/renderer/modules/crypto` | واجهة `WebCrypto` (`crypto.subtle`) لتطبيقات الويب |
| `blink/renderer/modules/clipboard` | واجهة الحافظة البرمجية `navigator.clipboard` |
| `blink/renderer/modules/mojo` | نقل الرسائل لبيئة التشغيل |
| `blink/renderer/modules/exported` | تصدير وحدات Blink المسموحة |
| `media/audio` | إدخال وإخراج ومزج الصوت في طبقة `media` |
| `media/base` | الهياكل الأساسية للإطارات الصوتية والمرئية والمخازن المؤقتة |
| `media/capabilities` | قاعدة قدرات فك الترميز |
| `media/ffmpeg` | ربط مفككات FFmpeg |
| `media/filters` | مرشحات فك التحزيم وفك ترميز الصوت والفيديو |
| `media/formats` | محللات حاويات MP4 وWebM وMPEG/AAC |
| `media/gfx` | تجمع إطارات الفيديو المشتركة مع GPU |
| `media/gpu` | فك وترميز الفيديو المسرّع عبر GPU |
| `media/mojo` | نقل تدفقات الوسائط بين العمليات |
| `media/muxers` | تجميع حاويات WebM/MP4 |
| `media/parsers` | محللات تدفقات البت VP8/VP9/AV1/H264 |
| `media/renderers` | مصيّر الصوت والفيديو المتزامن مع `cc`/`viz` |
| `media/video` | مكونات عرض ومعالجة إطارات الفيديو |
| `storage/browser` | التنفيذ الخلفي لـ Blob وQuota وFileSystem وDatabase |
| `storage/common` | الهياكل المشتركة لطبقة التخزين |
