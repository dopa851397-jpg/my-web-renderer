# my-web-renderer — مصدر عرض لتطبيقات ويب مبنية فقط (Chromium 158.0.8127.89)

هذا المستودع هو **مصدر عرض لتطبيقات ويب مبنية فقط (Web-App-Only Rendering Runtime Source)** مبني حصراً على إصدار Chromium المثبّت **`158.0.8127.89`** (`1de57fa19722fa6d6841d4f596c394d015580656`).

صُمِّمت هذه الشجرة المصدرية لتشغيل **تطبيقات ويب حديثة مكتفية ذاتياً** تُحمَّل أصولها محلياً عبر مخطط مثل `app://` وتتصل بخادمها الخاص فقط عبر `fetch` و`XMLHttpRequest` و`WebSocket` — **من دون أي واجهة متصفح تقليدية، ومن دون تصفح للمواقع الخارجية أو أدوات التتبع أو العتاد غير اللازم**.

---

## الوثائق المرجعية وسجلات التحقق في المستودع

- **[`KEEP_ROOTS.md`](KEEP_ROOTS.md)** — القائمة الكاملة للجذور الوحيدة المسموحة بمساراتها وأسباب الإبقاء عليها.
- **[`DOWNLOADS.md`](DOWNLOADS.md)** — سجل جميع الاعتماديات المنزّلة كأرشيفات بلا تاريخ Git (`+archive/<commit>.tar.gz`) مع الروابط والـ Commit والأحجام وبصمات `SHA256`.
- **[`NEEDED_DEPS.md`](NEEDED_DEPS.md)** — تحليل اعتماديات `third_party` المطلوبة والموجودة والمستبعدة.
- **[`CUT_DEPS.md`](CUT_DEPS.md)** — توثيق جميع الاعتماديات المقطوعة عمداً عند حدود الوحدات المحذوفة وأسباب قطعها.
- **[`REACHABLE.txt`](REACHABLE.txt) / [`UNREACHABLE.txt`](UNREACHABLE.txt)** — ناتج حساب الإغلاق التعدّي عبر `#include` و`BUILD.gn` و`DEPS`.
- **[`REMOVED.txt`](REMOVED.txt)** — سجل جميع الملفات المحذوفة بمساراتها وأحجامها (**339,051 ملفاً / 4134.42 MB**).
- **[`MISSING_INCLUDES.txt`](MISSING_INCLUDES.txt)** — التحقق النهائي من توجيهات `#include` بعد التقليم.

---

## المكونات الباقية وأحجامها

إجمالي الشجرة المصدرية الصافية بعد التقليم: **59,538 ملفاً** بحجم **849.61 MB** (مع الحفاظ الكامل على جميع ملفات التراخيص `LICENSE` / `COPYING` / `NOTICE` البالغ عددها **313 ملفاً** دون حذف أي ملف ترخيص، ودون تعديل أي سطر في الكود المصدري):

| المكون (المجلد) | عدد الملفات | الحجم الصافي | الوظيفة في بيئة تشغيل تطبيق الويب |
|---|---:|---:|---|
| `third_party/` | 11,445 | 259.42 MB | المكتبات الأساسية المثبّتة من `DEPS` (zlib, BoringSSL, Abseil, Protobuf, Perfetto, FreeType, libpng, libjpeg_turbo, libwebp, CrabbyAVIF, Brotli, Zstd, FFmpeg, libvpx, libaom, dav1d, Opus, FLAC, SQLite, LevelDB, SwiftShader، إلخ) |
| `icu/` | 5,780 | 127.07 MB | مكتبة Unicode والتدويل الكاملة مع بيانات وجداول اللغة العربية واتجاه النص من اليمين لليسار (RTL / UBiDi) |
| `blink/` | 12,722 | 83.90 MB | محرك عرض الويب Blink (HTML/DOM/CSS/Style/LayoutNG/Paint، SVG، Forms، Canvas، WebGL، WebAudio، Workers، Service Workers، IndexedDB، Fetch/WebSocket؛ مع حفظ ملفات `LICENSE` فقط في المجلدات المقلمة) |
| `v8/` | 3,571 | 69.57 MB | محرك JavaScript وWebAssembly الكامل (Ignition, Sparkplug, Maglev, TurboFan, Oilpan/Heap, Wasm) |
| `skia/` | 3,465 | 50.72 MB | محرك الرسم الثنائي الأبعاد والمسرّع عبر GPU (`Ganesh`/`Graphite`, `skcms`, `skshaper`, `skparagraph`, `skunicode`, `svg`) |
| `angle/` | 2,260 | 41.31 MB | طبقة ترجمة وتنفيذ OpenGL ES 2.0/3.0 وWebGL 1/2 (الرسم البرمجي + العتادي GL) |
| `net/` | 2,863 | 33.51 MB | مكدس الشبكة المقتصر على اتصال التطبيق بخادمه (`fetch`, `XHR`, `WebSocket`, HTTP/1.1–3, TLS, الكوكيز, الكاش) وتحميل أصول `app://` المحلية |
| `content/` | 2,638 | 23.32 MB | طبقة ربط العمليات الضرورية فقط (`renderer`، `gpu`، `child`، `common`، `utility`، ومضيفا `renderer_host`/`worker_host`/`service_worker`/التخزين) |
| `ui/` | 2,757 | 18.09 MB | طبقات النافذة والأحداث الرسومية لسطح المكتب (`gfx`, `gl`, `ozone`, `aura`, `events`, `compositor`, `color`, `display`) |
| `base/` | 2,120 | 13.30 MB | المكتبة التأسيسية (الخيوط، المجدولات، الذاكرة `PartitionAlloc`، الملفات، التوقيت، وتسجيل الأخطاء) |
| `media/` | 1,704 | 13.08 MB | أنابيب فك وترميز وتشغيل الصوت والفيديو المدمجة مع WebAudio و`<video>`/`<audio>` وWebCodecs |
| `gpu/` | 858 | 10.62 MB | مخزن الأوامر الرسومية وقنوات الاتصال مع معالج الرسوميات لـ Skia وWebGL |
| `components/` | 2,009 | 9.21 MB | خدمات ومكونات مساندة للتخزين والخطوط ومركّب العرض (`services/storage`, `services/font`, `viz` عبر الرابط الرمزي) |
| `services/` | 1,514 | 7.18 MB | الخدمات المعزولة اللازمة فقط (`network`, `viz`, `audio`, `data_decoder`, `service_manager/public`, `tracing/public`) |
| `harfbuzz/` | 574 | 6.99 MB | محرك تشكيل الحروف المتقدم OpenType (يشمل التشكيل العربي الكامل وRTL) |
| `cc/` | 694 | 5.90 MB | مركّب الطبقات والرسوم المتحركة والتقسيم البلاطي (`LayerTree`, `TileManager`) |
| `viz/` | 536 | 3.99 MB | خدمة وعميل تركيب الأسطح والإطارات النهائية (`DisplayCompositor`) |
| `mojo/` | 774 | 3.83 MB | نواة وواجهات الاتصال السريع بين العمليات (IPC) |
| `sandbox/` | 381 | 1.80 MB | آليات عزل عمليات الـ renderer والـ gpu على أنظمة سطح المكتب |
| `build/` | 245 | 1.65 MB | تعريفات المترجم والمنصة الأساسية (`build_config.h`, `compiler_specific.h`) |
| `storage/` | 232 | 1.64 MB | التنفيذ الخلفي لـ Blob وFileSystem وQuota وDatabase |
| `url/` | 76 | 0.53 MB | تحليل وتطبيع عناوين URL ودعم المخططات المخصصة مثل `app://` |
| `crypto/` | 94 | 0.53 MB | تغليف العمليات التشفيرية فوق BoringSSL |
| `sql/` | 37 | 0.38 MB | غلاف SQLite المستخدم في IndexedDB وCache Storage وQuota |
| `dbus/` | 31 | 0.31 MB | واجهات تكامل سطح مكتب Linux الأساسية |
| `gin/` | 74 | 0.27 MB | طبقة التغليف الخفيفة لربط عزلات V8 (`v8::Isolate`) |
| `ipc/` | 48 | 0.22 MB | قنوات الرسائل الأساسية المساندة لـ Mojo |
| `device/` | 26 | 0.06 MB | أنواع البيانات الأساسية المشتركة الباقية دون وحدات العتاد الممنوعة |

### الميزات القياسية المدعومة لتطبيقات الويب
- **العرض والتخطيط والواجهات:** HTML5، DOM، CSS3/LayoutNG، Paint، SVG، MathML، النماذج (Forms)، الأحداث، التحريك (Web Animations / CSS Animations).
- **البرمجة والحوسبة:** محرك **V8** الكامل لـ JavaScript (ESNext) و**WebAssembly (WASM)**.
- **الرسوميات المتقدمة:** **Canvas 2D**، `OffscreenCanvas`، **WebGL 1.0 / 2.0**، والرسم البرمجي والعتادي عبر **Skia** و**ANGLE** و**SwiftShader** و`cc` و`viz` و`gpu`.
- **النصوص واللغات:** دعم كامل للغة **العربية** واتجاه الكتابة من اليمين إلى اليسار (**RTL / BiDi**) وتشكيل الحروف عبر **HarfBuzz** و**ICU** و**FreeType**.
- **الصوت والوسائط:** **WebAudio**، عناصر `<audio>` و`<video>`، `MediaSource`، و**WebCodecs** (مع FFmpeg وOpus وFLAC وlibvpx وlibaom وdav1d).
- **التخزين والعمل بالخلفية:** **Workers** (`Worker`, `SharedWorker`, `Worklet`), **Service Workers**, **IndexedDB**, **Cache Storage**, `localStorage` / `sessionStorage`, ونظام الملفات المعزول OPFS.
- **الاتصال بالخادم وتحميل التطبيق:** `fetch()`, `XMLHttpRequest`, **WebSocket**, `EventSource`, وتحميل الملفات المحلية عبر مخطط `app://`.

---

## ما أُزيل ولماذا (حُذف 339,051 ملفاً / 4.04 GB)

أُزيل كل ما لا يلزم لبيئة عرض تطبيقات الويب المبنية، حتى لو وصلت إليه بعض الحواف الجانبية (وتم قطع الاعتماد وتوثيقه في [`CUT_DEPS.md`](CUT_DEPS.md)):

1. **واجهة المتصفح التقليدية:** التبويبات، شريط العنوان (`omnibox`)، سجل التصفح، الإشارات المرجعية، شاشات الإعدادات، صفحات `WebUI` (`chrome://*`)، وأدوات `ui/views` و`content/shell`. *(السبب: التطبيق يرسم واجهته الخاصة بالكامل بـ HTML/CSS/Canvas).*
2. **تصفح المواقع الخارجية والتتبع والشهادات العامة:** التنقل الخارجي والتنبؤ بالصفحات (`speculation_rules`, `preloading`, `fenced_frame`)، و`Safe Browsing`، ومخازن وواجهات شهادات المواقع العامة (`net/cert`, `cert_verifier`, `sct_auditing`, `pki`)، وأنظمة التتبع والإعلانات والقياسات (`ad_tracker`, `ad_auction`, `browsing_topics`, `attribution_reporting`, `ukm`, `metrics`, `variations`). *(السبب: البيئة مخصصة لتطبيق واحد معروف الخادم وليست متصفح إنترنت مفتوح).*
3. **الخدمات المكتبية والمتصفحية الثقيلة:** الإضافات (`extensions`)، عارض ومولّد `PDF`، الطباعة (`printing`)، الترجمة الآلية، الملء التلقائي (`autofill`)، المدفوعات (`payments`)، المزامنة (`sync`)، الحسابات (`signin`/`gaia`/`webid`)، والبث الخارجي (`Cast`).
4. **أدوات الفحص والتطوير (`DevTools` / `Inspector`):** حُذفت بالكامل من Blink و`content` وV8، مع **الإبقاء فقط على نقطة تسجيل أخطاء بسيطة** (`ConsoleMessage` في `blink/renderer/core/inspector/console_message.{h,cc}`).
5. **واجهات العتاد والميزات الممنوعة:** حُذفت بالكامل `WebRTC`، `WebGPU` / `Dawn`، `WebXR` / `VR`، وواجهات العتاد (`Bluetooth`, `WebUSB`, `Serial`, `HID`, `NFC`, `MIDI`, `SmartCard`, `Sensor`, `Geolocation`), و`Notifications` / `Push`، و`Payment Request`، و`WebAuthn` / `Credentials` / `FIDO`، و`Presentation`، و`Idle Detection`، و`WebShare` / `Contacts`.
6. **الاختبارات والتوثيق والأمثلة والـ Fuzzers:** حُذفت جميع مجموعات `blink/web_tests` (~200 ألف ملف)، واختبارات الوحدات والمتصفح والأداء، وملفات `testdata`، وبذور الـ `fuzzers`، والأمثلة، والتوثيق الفرعي *(مع عدم المساس بأي ملف ترخيص `LICENSE`/`COPYING`/`NOTICE`)*.
7. **المنصات غير المدعومة:** حُذفت جميع مسارات وملفات **Android** و**iOS** و**ChromeOS / Ash** و**Fuchsia**.
