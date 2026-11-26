# NEEDED_DEPS.md — فحص اعتماديات `third_party` للمشروع (Chromium 158.0.8127.89)

تم فحص جميع المجلدات الخمسة عشر الموجودة في المستودع (`blink`, `v8`, `skia`, `net`, `content`, `cc`, `viz`, `gpu`, `base`, `mojo`, `services`, `url`, `angle`, `icu`, `harfbuzz`) نصياً عبر توجيهات `#include` وملفات `BUILD.gn`/`.gni` وملفات `DEPS`، ومطابقتها مع `chromium-158.0.8127.89.DEPS` وشجرة `chromium/src` عند الالتزام المثبّت `1de57fa19722fa6d6841d4f596c394d015580656` (الوسم `158.0.8127.89`).

## 1. اعتماديات `third_party` المطلوبة للتنزيل (تُنزَّل في الخطوة 3)

| # | الاعتمادية (المسار) | من يطلبها (`#include` / `BUILD.gn` / `DEPS`) | المصدر والـ Commit المثبّت | سبب الاحتياج |
|---:|---|---|---|---|
| 1 | `third_party/zlib` | `#include`: base, blink, content, gpu, harfbuzz, net, services, skia, v8, viz ؛ `BUILD.gn`: angle, base, blink, content, gpu, net, services, skia, v8, viz ؛ `DEPS`: angle, base, blink, content, gpu, net, services, v8, viz | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | ضغط وفك ضغط البيانات (HTTP gzip/deflate، PNG، Blink، Skia، V8، net) |
| 2 | `third_party/boringssl` | `#include`: base, blink, content, net, services ؛ `BUILD.gn`: base, blink, content, net, services ؛ `DEPS`: base, blink, content, net, services | chromium/src + boringssl.git @ `ea9f3a34c3977144c45d272be81842fd891a0bdb` | تشفير TLS/HTTPS وWebSockets الآمنة (wss://) وWebCrypto |
| 3 | `third_party/abseil-cpp` | `#include`: angle, base, blink, cc, content, gpu, mojo, net, services, skia, url, v8, viz ؛ `BUILD.gn`: angle, base, blink, cc, content, mojo, net, services, v8 ؛ `DEPS`: angle, base, mojo, v8 | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | أنواع وحاويات C++ الأساسية المستخدمة في جميع طبقات المحرك |
| 4 | `third_party/protobuf` | `#include`: base, blink, gpu, mojo, net, services ؛ `BUILD.gn`: base, blink, content, gpu, mojo, net, services ؛ `DEPS`: angle, base, blink, gpu, mojo, net, services, v8 | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | وقت تشغيل Protocol Buffers الخفيف (protobuf_lite) للرسائل الداخلية |
| 5 | `third_party/perfetto` | `#include`: angle, base, blink, cc, content, gpu, mojo, net, services, skia, v8, viz ؛ `BUILD.gn`: angle, base, content, net, services, skia, v8 ؛ `DEPS`: angle, base, blink, cc, content, mojo, services, v8, viz | perfetto.git @ `214c983f4c72c442d71415d9c81a7e1ed11566a7` | رؤوس وماكروهات التتبع الأساسية (`TRACE_EVENT`) في base وblink وcc وgpu وv8 |
| 6 | `third_party/brotli` | `#include`: net ؛ `BUILD.gn`: content, net, skia ؛ `DEPS`: net | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | فك ضغط Brotli للاستجابات الشبكية (`fetch`/XHR) وخطوط WOFF2 |
| 7 | `third_party/zstd` | `#include`: blink, content, net, services ؛ `BUILD.gn`: angle, blink, content, net, services ؛ `DEPS`: angle, blink, content, net, services | chromium/src + zstd.git @ `10da6ba6de05e29169261fa4b68eb99239f770dd` | فك ضغط Zstandard في طبقة الشبكة `net` و`services/network` |
| 8 | `net/third_party/quiche` | `#include`: content, net, services ؛ `BUILD.gn`: net ؛ `DEPS`: blink | quiche.git @ `132bfd90ea370faeacee616c70d10210bb12ba66` (داخل `net/third_party/quiche/src`) | إطارات HTTP/2 (SPDY/HPACK) وHTTP/3 وWebSocket فوق HTTP/2-3 لطلبات `fetch`/XHR/WebSocket |
| 9 | `third_party/ipcz` | `#include`: mojo ؛ `BUILD.gn`: mojo ؛ `DEPS`: mojo | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | نواة نقل الرسائل بين العمليات في `mojo` |
| 10 | `third_party/freetype` | `#include`: harfbuzz, skia ؛ `BUILD.gn`: skia | chromium/src + freetype2.git @ `a5877f48fff8dd6cf8d53c505ce055499376aee2` | تصيير الخطوط الأساسي لـ Skia وBlink وHarfBuzz |
| 11 | `third_party/harfbuzz` | `BUILD.gn`: blink, skia | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` (ملفات الربط `BUILD.gn`؛ الكود المصدري موجود في `harfbuzz/`) | ربط GN لمكتبة تشكيل النصوص العربية وRTL |
| 12 | `third_party/woff2` | `#include`: blink ؛ `BUILD.gn`: blink | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | فك ضغط خطوط الويب بصيغة WOFF2 في Blink |
| 13 | `third_party/ots` | `#include`: blink ؛ `BUILD.gn`: blink | chromium/src + ots.git @ `46bea9879127d0ff1c6601b078e2ce98e83fcd33` | التحقق من سلامة خطوط الويب OpenType (`@font-face`) في Blink |
| 14 | `third_party/emoji-segmenter` | `#include`: blink ؛ `BUILD.gn`: blink | chromium/src + emoji-segmenter.git @ `955936be8b391e00835257059607d7c5b72ce744` | تقسيم الرموز التعبيرية (Emoji) أثناء تخطيط النصوص في Blink |
| 15 | `third_party/fontconfig` | `#include`: content, harfbuzz, skia ؛ `BUILD.gn`: content | chromium/src + fontconfig.git @ `d416ada7b20a1cdd5050b60a7a1bbdb3d9ddd2dc` | اكتشاف ومطابقة الخطوط على Linux |
| 16 | `third_party/libpng` | `#include`: angle, harfbuzz, skia ؛ `BUILD.gn`: angle, skia ؛ `DEPS`: angle | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | ترميز وفك ترميز صور PNG للـ DOM وCanvas وSkia |
| 17 | `third_party/libjpeg_turbo` | `#include`: blink, skia ؛ `BUILD.gn`: skia | libjpeg_turbo.git @ `640f254ad0fa03f6b1f29f89b7dd9366f2f6e533` | ترميز وفك ترميز صور JPEG في Blink وSkia |
| 18 | `third_party/libwebp` | `#include`: blink, skia ؛ `BUILD.gn`: blink, skia | chromium/src + libwebp.git @ `68dd1c3040d500f56fe7ffb754b1813fb64b5887` | ترميز وفك ترميز صور WebP في Blink وSkia |
| 19 | `third_party/crabbyavif` | `#include`: blink ؛ `BUILD.gn`: blink | chromium/src + CrabbyAvif.git @ `40732a9090353e3dae550b77d799a0ce5c7a3c29` | فك ترميز صور AVIF في Blink |
| 20 | `third_party/wuffs` | `BUILD.gn`: skia | chromium/src + wuffs.git @ `3bbda65fd6e7266f6cd80bc48f0c7ebce4e8f24b` | فك ترميز صور GIF الآمن في Skia وBlink |
| 21 | `third_party/libyuv` | `#include`: blink, content, gpu, viz ؛ `BUILD.gn`: blink, content, gpu, skia, viz ؛ `DEPS`: blink, cc, content, gpu, viz | libyuv.git @ `1e2e3a35993609da1d89ac170b907719d555f4b3` | تحويلات الفضاء اللوني YUV/RGB لـ Canvas والفيديو وWebGL وViz |
| 22 | `third_party/leveldatabase` | `#include`: content ؛ `BUILD.gn`: content ؛ `DEPS`: content | chromium/src + leveldb.git @ `bb74ef739973a70ca9f0d90788a1da89b788c0ad` | محرك التخزين الخلفي لـ IndexedDB وlocalStorage وService Workers |
| 23 | `third_party/snappy` | `#include`: blink, content, services ؛ `BUILD.gn`: blink, content, services ؛ `DEPS`: content, services | chromium/src + snappy.git @ `32ded457c0b1fe78ceb8397632c416568d6714a0` | ضغط سريع لبيانات LevelDB/IndexedDB وCache Storage |
| 24 | `third_party/sqlite` | `#include`: content ؛ `BUILD.gn`: content, net ؛ `DEPS`: content | chromium/src + sqlite.git @ `c1172ac3c91edb02a86ea9ce479ef5b5fe5c6f34` | محرك قواعد البيانات لتخزين الكاش وQuota وملفات تعريف الارتباط |
| 25 | `third_party/liburlpattern` | `#include`: blink, content ؛ `BUILD.gn`: blink, services ؛ `DEPS`: blink, content | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | واجهة `URLPattern` القياسية وتوجيه Service Workers في Blink وcontent |
| 26 | `third_party/re2` | `#include`: blink, content, gpu, net, services ؛ `BUILD.gn`: angle, blink, content, gpu, net, services ؛ `DEPS`: angle, blink, content, gpu, net, services, v8 | chromium/src + re2.git @ `2da0056814cf180480a19f5cf811e7e1c054bf6d` | محرك التعابير النمطية لـ URLPattern والنماذج (forms) والشبكة |
| 27 | `third_party/modp_b64` | `#include`: base, blink ؛ `BUILD.gn`: base, blink ؛ `DEPS`: base | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | ترميز وفك ترميز Base64 السريع (`atob`/`btoa`، الروابط البيانية `data:`) |
| 28 | `third_party/simdutf` | `#include`: base, blink, net ؛ `BUILD.gn`: base, blink, net, v8 ؛ `DEPS`: base, net, v8 | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | تحويل والتحقق من نصوص UTF-8/UTF-16 بتسريع SIMD في base وblink وnet وv8 |
| 29 | `third_party/rapidhash` | `#include`: blink ؛ `BUILD.gn`: blink | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | دوال تجزئة سريعة في Blink |
| 30 | `third_party/ced` | `#include`: base, blink ؛ `BUILD.gn`: base, blink, content ؛ `DEPS`: base, blink | chromium/src + compact_enc_det.git @ `d127078cedef9c6642cbe592dacdd2292b50bb19` | كشف ترميز النصوص لملفات HTML/CSS/JS |
| 31 | `third_party/libxml` | `#include`: base, blink, services ؛ `BUILD.gn`: angle, base, blink, services ؛ `DEPS`: base, services | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | محلل XML وSVG في Blink |
| 32 | `third_party/libxslt` | `#include`: blink ؛ `BUILD.gn`: blink | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | دعم XSLT المرتبط بمحلل XML في Blink |
| 33 | `third_party/expat` | `#include`: angle, skia ؛ `BUILD.gn`: angle, skia ؛ `DEPS`: angle | chromium/src + libexpat.git @ `a851869e111c06fbcdc89edf639abf5fc2b6deba` | محلل XML الخفيف لـ Fontconfig وSkia وANGLE |
| 34 | `third_party/fdlibm` | `#include`: blink ؛ `BUILD.gn`: blink ؛ `DEPS`: v8 | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | الدوال الرياضية القياسية الحتمية لـ WebAudio في Blink |
| 35 | `third_party/eigen3` | `#include`: blink | chromium/src + eigen.git @ `7177d997a36148ac1cecb26e3cda8fa0ef35711e` | عمليات الجبر الخطي لمعالجة الصوت في WebAudio |
| 36 | `third_party/opus` | `#include`: blink ؛ `BUILD.gn`: blink ؛ `DEPS`: blink | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | ترميز وفك ترميز الصوت Opus لـ WebAudio وMedia |
| 37 | `third_party/flac` | `BUILD.gn`: content ؛ `DEPS`: content | flac.git @ `e7108e2ed031547c3759217819a032065c820d73` | فك ترميز الصوت FLAC في Media وWebAudio |
| 38 | `third_party/libvpx` | `#include`: blink ؛ `BUILD.gn`: blink ؛ `DEPS`: blink | chromium/src + libvpx.git @ `fb1279dcc6db0cbfb0b6015d0ba7587759c5625a` | فك ترميز الفيديو VP8/VP9 لعناصر `<video>` وMedia |
| 39 | `third_party/libgav1` | `#include`: blink ؛ `BUILD.gn`: blink, skia | chromium/src + libgav1.git @ `c3c824dcc1b907eed484f88ca7af21c743d27494` | فك ترميز الفيديو AV1 في Blink وMedia |
| 40 | `third_party/dav1d` | غير مباشر | chromium/src + dav1d.git @ `9433da2daa61bf7029a52b84bafa5daf59cdcc9d` | مفكك AV1 السريع في Media |
| 41 | `third_party/libwebm` | غير مباشر | chromium/src + libwebm.git @ `a7c6662c68a90af18dd53dbb1f4262a346e9a547` | تحليل حاويات WebM الصوتية والمرئية |
| 42 | `third_party/ffmpeg` | `#include`: skia | ffmpeg.git @ `42a2a7a2b2ceb0b1554af1e99a8cdaae189404bb` | فك تحزيم وترميز الوسائط القياسية لـ Media وWebAudio |
| 43 | `third_party/fp16` | `#include`: blink, services, v8 ؛ `BUILD.gn`: blink, services, v8 ؛ `DEPS`: services, v8 | chromium/src + FP16.git @ `782eea126dc5c755827be751a099eb01826175cf` | تحويلات الأعداد العشرية نصف الدقة `Float16Array` في V8 وCanvas/WebGL |
| 44 | `third_party/highway` | `#include`: blink ؛ `BUILD.gn`: blink, skia, v8 ؛ `DEPS`: v8 | chromium/src + highway.git @ `2607d3b5b0113992fe84d3848859eae13b3b52c1` | تعليمات SIMD المحمولة المستخدمة في V8 وBlink وSkia |
| 45 | `third_party/dragonbox` | `#include`: v8 ؛ `BUILD.gn`: v8 ؛ `DEPS`: v8 | chromium/src + dragonbox.git @ `beeeef91cf6fef89a4d4ba5e95d47ca64ccb3a44` | تحويل الأعداد العشرية إلى نصوص في محرك V8 |
| 46 | `third_party/fast_float` | `#include`: v8 ؛ `BUILD.gn`: v8 ؛ `DEPS`: v8 | chromium/src + fast_float.git @ `42f254836ee416ffcf2f4e6576260003ac33d48c` | تحويل النصوص إلى أعداد عشرية بسرعة عالية في V8 |
| 47 | `third_party/disarm` | `#include`: v8 ؛ `BUILD.gn`: v8 ؛ `DEPS`: v8 | chromium/src + disarm.git @ `2d960dae4b4fb29dba05cfc48210fbed423f3d2c` | مفكك تعليمات ARM64 لمولد الكود في V8 |
| 48 | `third_party/fadec` | `#include`: v8 ؛ `BUILD.gn`: v8 ؛ `DEPS`: v8 | chromium/src + fadec.git @ `c9f78f532b9004de278489019ab2c6c28ae9746e` | مفكك تعليمات x86-64 لمولد الكود في V8 |
| 49 | `third_party/llvm-libc` | `#include`: v8 ؛ `BUILD.gn`: v8 ؛ `DEPS`: angle, v8 | chromium/src + libc.git @ `567c143bea85f11d15702a120561a8e51f46f02c` | الدوال الرياضية المشتركة (`shared/math.h`) المطلوبة في V8 |
| 50 | `third_party/rust` | `#include`: base, blink, content, mojo, net, services, skia, url ؛ `BUILD.gn`: base, blink, content, mojo, net, services, url, v8 ؛ `DEPS`: angle, base, content, mojo, net, services, url, v8 | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` (الحزم الجزئية اللازمة فقط: `cxx`، `temporal_capi`، `icu_capi`، `serde_json_lenient`، `sfv`، `diplomat-runtime`) | رؤوس الربط C++/Rust لكائنات `Temporal` في V8 وتطبيع النصوص وتحليل JSON/HTTP |
| 51 | `third_party/swiftshader` | `BUILD.gn`: angle ؛ `DEPS`: angle, gpu | SwiftShader.git @ `cddb5c91b23ff70a1f607ea31610aa0d7f4b5ad5` | التصيير البرمجي لـ OpenGL ES / WebGL مع ANGLE (برمجي + GL) |
| 52 | `third_party/vulkan-headers` | `BUILD.gn`: angle, gpu ؛ `DEPS`: angle, gpu, viz | chromium/src + Vulkan-Headers @ `73814d006638aa00bd553215b054f0f02e457e22` | رؤوس تعريفات Vulkan لـ GPU وViz وANGLE وSkia |
| 53 | `third_party/vulkan_memory_allocator` | `BUILD.gn`: angle, gpu ؛ `DEPS`: angle | VulkanMemoryAllocator.git @ `82a9d47e4f9d91f0e32d2b6acd9714fcee1933a0` | مخصص الذاكرة الرسومية لـ GPU وANGLE وSkia |
| 54 | `third_party/spirv-headers` | `BUILD.gn`: angle ؛ `DEPS`: angle | chromium/src + SPIRV-Headers @ `fbf86836a9b1966586faf7be7bb8a6440e156d62` | رؤوس SPIR-V لمترجم المظللات في ANGLE |
| 55 | `third_party/libsync` | `BUILD.gn`: gpu | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | مزامنة إطارات الرسم في `gpu` |
| 56 | `third_party/libdrm` | `#include`: gpu ؛ `DEPS`: angle, gpu | chromium/src + libdrm.git @ `e984d448b8b17aab853369e6c203e53719f46de1` | تعريفات مخازن الإطارات الرسومية DRM على Linux لـ `gpu` و`angle` |
| 57 | `third_party/wayland` | `BUILD.gn`: angle, gpu ؛ `DEPS`: angle | chromium/src + wayland.git @ `87cc8a8728a923fc57938faa81ba0e74f34ecdc7` | دعم نوافذ وسطح العرض Wayland على Linux لـ `gpu` و`angle` |
| 58 | `third_party/wayland-protocols` | `BUILD.gn`: angle ؛ `DEPS`: angle | chromium/src + wayland-protocols.git @ `ee78491a237eaff9389a0ccf8680521d074407d3` | بروتوكولات Wayland القياسية للعرض الرسومي |
| 59 | `third_party/microsoft_dxheaders` | `#include`: gpu ؛ `BUILD.gn`: gpu ؛ `DEPS`: gpu | chromium/src + DirectX-Headers.git @ `07b94cba474be6cdfd934febdbd0b21ca0524187` | رؤوس DirectX 12 / DXCore لطبقة `gpu` على Windows |
| 60 | `third_party/one_euro_filter` | `BUILD.gn`: blink | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | تنعيم أحداث الإدخال والمؤشر في Blink |
| 61 | `third_party/lss` | `#include`: base ؛ `DEPS`: base | linux-syscall-support.git @ `29164a80da4d41134950d76d55199ea33fbb9613` | رؤوس استدعاءات النظام منخفضة المستوى على Linux في `base` |
| 62 | `third_party/cpuinfo` | `#include`: content ؛ `BUILD.gn`: content ؛ `DEPS`: content | chromium/src + cpuinfo.git @ `66ee79c038d70dad9f08705b2c9b3e58f6d8f512` | استعلام خصائص المعالج في `content` |
| 63 | `third_party/apple_apsl` | `#include`: net ؛ `DEPS`: base, net | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | رؤوس DNS والذاكرة لنظام macOS في `net` و`base` |
| 64 | `third_party/libaom` | `BUILD.gn`: blink ؛ `DEPS`: blink, content | chromium/src + aom.git @ `8f126544519961bb3d5afe83455f4caf5d312d05` | مفكك ومُرمّز فيديو AV1 في `media/video` وBlink |
| 65 | `third_party/material_color_utilities` | غير مباشر | chromium/src + material-color-utilities.git @ `dd62982dfdefdfc9232ce8d76e122fb1c6d188ae` | حساب لوحات الألوان في `ui/color` |
| 66 | `third_party/iaccessible2` | `#include`: content ؛ `BUILD.gn`: content ؛ `DEPS`: content | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | تعريفات واجهة الوصول الأساسية في `ui/accessibility` على Windows |
| 67 | `third_party/isimpledom` | `#include`: content ؛ `BUILD.gn`: content ؛ `DEPS`: content | chromium/src @ `1de57fa19722fa6d6841d4f596c394d015580656` | تعريفات واجهة الوصول لـ DOM في `ui/accessibility` على Windows |

## 2. اعتماديات `third_party` الموجودة مسبقاً في المستودع

| # | الاعتمادية | من يطلبها | الحالة والموقع المحلي |
|---:|---|---|---|
| 1 | `third_party/blink` | `#include`: blink, cc, content, gpu, mojo, services, viz ؛ `BUILD.gn`: blink, cc, content, gpu, mojo, services, url, viz ؛ `DEPS`: blink, cc, content, gpu, mojo, services, viz | موجود في الجذر `blink/` (وسيُربط بمساره المعياري `third_party/blink`) |
| 2 | `third_party/skia` | `#include`: blink, cc, content, gpu, services, skia, viz ؛ `BUILD.gn`: gpu ؛ `DEPS`: blink, cc, content, gpu, services, viz | موجود في الجذر `skia/` (وسيُربط بمساره المعياري `third_party/skia`) |
| 3 | `third_party/angle` | `#include`: blink, cc, content, gpu, viz ؛ `BUILD.gn`: blink, cc, content, gpu, services, viz ؛ `DEPS`: blink, cc, content, gpu, viz | موجود في الجذر `angle/` (وسيُربط بمساره المعياري `third_party/angle`) |
| 4 | `third_party/icu` | `#include`: base, blink, content, icu, net, services, url ؛ `BUILD.gn`: base, blink, content, icu, net, services, skia, url, v8 ؛ `DEPS`: blink, net, url, v8 | موجود في الجذر `icu/` (وسيُربط بمساره المعياري `third_party/icu`) |
| 5 | `harfbuzz (third_party/harfbuzz/src)` | غير مباشر | موجود في الجذر `harfbuzz/` (وسيُربط بـ `third_party/harfbuzz/src` و`third_party/harfbuzz-ng/src`) |
| 6 | `base/third_party/cityhash` | `#include`: base ؛ `BUILD.gn`: base | موجود داخل `base/third_party/cityhash` |
| 7 | `base/third_party/cityhash_v103` | `#include`: base ؛ `BUILD.gn`: base | موجود داخل `base/third_party/cityhash_v103` |
| 8 | `base/third_party/double_conversion` | `#include`: base, blink ؛ `BUILD.gn`: base, blink ؛ `DEPS`: blink | موجود داخل `base/third_party/double_conversion` |
| 9 | `base/third_party/icu` | `#include`: base, content, net, url ؛ `BUILD.gn`: base | موجود داخل `base/third_party/icu` |
| 10 | `base/third_party/nspr` | `#include`: base | موجود داخل `base/third_party/nspr` |
| 11 | `base/third_party/symbolize` | `#include`: base ؛ `BUILD.gn`: base | موجود داخل `base/third_party/symbolize` |
| 12 | `base/third_party/xdg_user_dirs` | `#include`: base ؛ `BUILD.gn`: base | موجود داخل `base/third_party/xdg_user_dirs` |
| 13 | `base/third_party/superfasthash` | `BUILD.gn`: base | موجود داخل `base/third_party/superfasthash` |
| 14 | `partition_alloc/third_party/apple_apsl` | `#include`: base | موجود داخل `base/allocator/partition_allocator/src/partition_alloc/third_party/apple_apsl` |
| 15 | `third_party/partition_alloc` | `#include`: v8 ؛ `BUILD.gn`: angle, v8 ؛ `DEPS`: angle, v8 | موجود داخل `base/allocator/partition_allocator` |
| 16 | `net/third_party/mozilla_security_manager` | `#include`: net | موجود داخل `net/third_party/mozilla_security_manager` |
| 17 | `net/third_party/mozilla_win` | `#include`: net | موجود داخل `net/third_party/mozilla_win` |
| 18 | `net/third_party/uri_template` | `#include`: net ؛ `BUILD.gn`: net | موجود داخل `net/third_party/uri_template` |
| 19 | `url/third_party/mozilla` | `#include`: blink, content, net, services, url | موجود داخل `url/third_party/mozilla` |
| 20 | `third_party/rapidhash-v8` | `#include`: v8 ؛ `DEPS`: v8 | موجود داخل `v8/third_party/rapidhash-v8` |
| 21 | `third_party/siphash` | `#include`: v8 ؛ `DEPS`: v8 | موجود داخل `v8/third_party/siphash` |
| 22 | `third_party/utf8-decoder` | `#include`: v8 ؛ `DEPS`: v8 | موجود داخل `v8/third_party/utf8-decoder` |
| 23 | `third_party/v8` | `#include`: v8 ؛ `DEPS`: v8 | موجود داخل `v8/third_party/v8` |
| 24 | `third_party/valgrind` | `#include`: v8 ؛ `DEPS`: v8 | موجود داخل `v8/third_party/valgrind` |
| 25 | `third_party/vtune` | `#include`: v8 ؛ `DEPS`: v8 | موجود داخل `v8/third_party/vtune` |
| 26 | `v8/third_party/vtune` | `#include`: content ؛ `DEPS`: content | موجود داخل `v8/third_party/vtune` |
| 27 | `third_party/wasm-api` | `#include`: v8 ؛ `DEPS`: v8 | موجود داخل `v8/third_party/wasm-api` (واجهة WebAssembly C/C++) |
| 28 | `third_party/etc1` | `#include`: skia | موجود داخل `skia/third_party/etc1` |
| 29 | `third_party/vello` | `#include`: skia ؛ `BUILD.gn`: skia | موجود داخل `skia/third_party/vello` |
| 30 | `third_party/externals` | `#include`: skia ؛ `BUILD.gn`: skia ؛ `DEPS`: skia | مسار داخلي اختياري لبناء Skia المستقل (`skia/third_party`) |
| 31 | `include/third_party/vulkan` | `#include`: skia | موجود داخل `skia/include/third_party/vulkan` |
| 32 | `third_party/ceval` | `#include`: angle | موجود داخل `angle/src/third_party/ceval` |
| 33 | `third_party/libXNVCtrl` | `#include`: angle | موجود داخل `angle/src/third_party/libXNVCtrl` |

## 3. مجلدات مساندة من `chromium/src` (نفس الالتزام المثبّت `1de57fa19722fa6d6841d4f596c394d015580656`) لازمة لحل `#include` للمكونات المسموحة

بما أن المجلدات الخمسة عشر تعتمد مباشرة عبر `#include "..."` على طبقات مساندة من نفس شجرة `chromium/src` (ليست متصفحاً بل بنية رسوم/صوت/تخزين/تشفير/IPC)، يلزم تنزيل الأجزاء الناقصة التالية فقط دون تنزيل Chromium كاملاً:

| المسار في `chromium/src` | من يطلبها | الدور |
|---|---|---|
| `ui/gfx`, `ui/gl`, `ui/events`, `ui/base`, `ui/display`, `ui/latency`, `ui/color`, `ui/native_theme`, `ui/accessibility`, `ui/compositor`, `ui/aura`, `ui/aura_extra`, `ui/ozone`, `ui/platform_window`, `ui/touch_selection`, `ui/shell_dialogs`, `ui/menus`, `ui/wm`, `ui/linux`, `ui/snapshot`, `ui/accelerated_widget_mac`, `ui/strings` | `blink`, `cc`, `viz`, `gpu`, `content`, `services` | الهندسة الرياضية (`gfx::Rect`/`Transform`)، ربط GL، أحداث الإدخال، العرض والسمات |
| `media/{audio,base,capabilities,capture,device_monitors,ffmpeg,filters,formats,gfx,gpu,mojo,muxers,parsers,renderers,video}` | `blink`, `content`, `services`, `cc`, `gpu`, `viz` | خط أنابيب الصوت والفيديو لـ WebAudio وعناصر `<audio>`/`<video>` |
| `storage/{browser,common}` | `blink`, `content`, `services` | إدارة Blob وQuota وFileSystem وDatabase اللازمة لـ IndexedDB وCache API وlocalStorage |
| `crypto` | `base`, `net`, `blink`, `content`, `services` | واجهات التشفير الأساسية فوق BoringSSL |
| `gin` | `blink`, `content`, `services` | طبقة الربط القياسية بين محرك V8 وC++ |
| `ipc` | `blink`, `cc`, `content`, `gpu`, `mojo`, `services`, `url`, `viz` | قنوات الاتصال بين عمليتي renderer وgpu |
| `sql` | `content`, `net`, `services` | غلاف Chromium الآمن فوق SQLite للتخزين |
| `sandbox/{linux,mac,policy,win}` + رؤوس الجذر | `content`, `gpu`, `services` | عزل عمليتي renderer وgpu |
| `skia/{config,ext,public}` | `blink`, `cc`, `content`, `gpu`, `services`, `viz` | ملفات التكيف (`skia/ext/*`) وسمات Mojo لـ Skia في Chromium |
| `dbus` + `device/{base,gamepad,udev_linux}` | `net`, `services`, `content`, `blink`, `cc` | مراقبة حالة الشبكة/النظام على Linux وتجريد الأجهزة الأساسية غير الممنوعة |
| مجلدات `components/` الأساسية غير المتصفحية (`input`, `services/{storage,font,font_data,filesystem,heap_profiling,quarantine,unzip}`, `discardable_memory`, `persistent_cache`, `os_crypt`, `prefs`, `pref_registry`, `url_formatter`, `url_pattern`, `url_matcher`, `link_header_util`, `web_package`, `cbor`, `sqlite_vfs`, `sqlite_proto`, `leveldb_proto`, `keyed_service`, `memory_pressure`, `memory_system`, `webcrypto`, `version_info`, `origin_trials`, `origin_matcher`, `embedder_support`, `network_session_configurator`, `file_access`, `power_monitor`, `system_cpu`, `vrp_flags`, `base32`, `cookie_config`, `content_settings`, `web_cache`, `metal_util`, `winhttp`, `dbus`, `value_store`, `variations`, `metrics`, `crash`, `tracing`, `performance_manager`, `startup_metric_utils`, `device_event_log`, `filename_generation`, `app_launch_prefetch`, `application_locale_storage`, `language`, `network_time`, `network_hints`, `system_media_controls`, `custom_handlers`, `back_forward_cache`, `browsing_data`, `vector_icons`, `surface_embed`, `session_manager`) | `blink`, `content`, `net`, `services`, `gpu`, `viz`, `cc` | خدمات التخزين (`IndexedDB`/`DOMStorage`/`Cache`)، الخطوط، الإدخال، الذاكرة القابلة للتفريغ، وWebCrypto |

## 4. اعتماديات `third_party` غير المطلوبة (مستبعدة ولن تُنزَّل)

الجدول التالي يغطي **كل** اعتمادية أخرى وردت في `#include` أو `BUILD.gn` أو `DEPS` مع سبب عدم الحاجة إليها:

| # | الاعتمادية | أين وردت (`#include` / `BUILD.gn` / `DEPS`) | القرار والسبب |
|---:|---|---|---|
| 1 | `buildtools/third_party/libc` | `BUILD.gn`: angle, base, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 2 | `chromium/third_party/android_build_tools` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 3 | `chromium/third_party/android_deps` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 4 | `chromium/third_party/android_sdk` | `DEPS`: angle, v8 | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 5 | `chromium/third_party/android_system_sdk` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 6 | `chromium/third_party/android_toolchain` | `DEPS`: angle, v8 | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 7 | `chromium/third_party/jdk` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 8 | `chromium/third_party/r8` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 9 | `chromium/third_party/turbine` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 10 | `test_utils/third_party/vulkan_command_buffer_utils.h` | `#include`: angle | غير مطلوب — أداة اختبار داخل `angle/src/tests` (تُحذف مع الاختبارات في الخطوة 8) |
| 11 | `third_party/EGL-Registry` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 12 | `third_party/OpenCL-CTS` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 13 | `third_party/OpenCL-Docs` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 14 | `third_party/OpenCL-ICD-Loader` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 15 | `third_party/OpenGL-Registry` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 16 | `third_party/Python-Markdown` | `DEPS`: angle | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 17 | `third_party/VK-GL-CTS` | `DEPS`: angle | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 18 | `third_party/android_build_tools` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 19 | `third_party/android_deps` | `BUILD.gn`: base, cc, content, net, services, url ؛ `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 20 | `third_party/android_ndk` | `BUILD.gn`: v8 | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 21 | `third_party/android_platform` | `DEPS`: angle, v8 | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 22 | `third_party/android_sdk` | `BUILD.gn`: base, content, net ؛ `DEPS`: angle, v8 | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 23 | `third_party/android_system_sdk` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 24 | `third_party/android_toolchain` | `#include`: content ؛ `DEPS`: angle, content, v8 | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 25 | `third_party/androidx` | `BUILD.gn`: base, blink, cc, content, mojo, net, services, url, viz | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 26 | `third_party/angle2` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 27 | `third_party/anonymous_tokens` | `BUILD.gn`: net | غير مطلوب — خاص بتتبع الإعلانات/Trust Tokens غير المطلوبة |
| 28 | `third_party/aria-practices` | `BUILD.gn`: content | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 29 | `third_party/astc-encoder` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 30 | `third_party/breakpad` | `BUILD.gn`: content | غير مطلوب — خدمة تقارير الأعطال للمتصفح غير مطلوبة |
| 31 | `third_party/catapult` | `BUILD.gn`: angle, blink, content, mojo, v8 ؛ `DEPS`: angle, v8 | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 32 | `third_party/cherry` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 33 | `third_party/clang-format` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 34 | `third_party/closure_compiler` | `BUILD.gn`: mojo | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 35 | `third_party/clspv` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 36 | `third_party/colorama` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 37 | `third_party/coremltools` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — أدوات WebNN/CoreML غير المطلوبة |
| 38 | `third_party/cpu-features` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 39 | `third_party/cpu_features` | `BUILD.gn`: base, blink, content ؛ `DEPS`: angle, v8 | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 40 | `third_party/cpython3` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 41 | `third_party/crashpad` | `BUILD.gn`: content | غير مطلوب — خدمة تقارير الأعطال للمتصفح غير مطلوبة |
| 42 | `third_party/cros_system_api` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: content, services | غير مطلوب — خاص بمنصة ChromeOS غير المدعومة (الخطوة 8) |
| 43 | `third_party/d3d12allocator` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 44 | `third_party/dawn` | `#include`: blink, cc, content, gpu, services, viz ؛ `BUILD.gn`: angle, blink, cc, content, gpu, services, skia, viz ؛ `DEPS`: angle, cc, content, gpu, services, viz | غير مطلوب — ميزة WebGPU ممنوعة صراحةً (الخطوة 8) |
| 45 | `third_party/delaunator` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 46 | `third_party/depot_tools` | `BUILD.gn`: angle ؛ `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 47 | `third_party/dng_sdk` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 48 | `third_party/dummy_chromium` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 49 | `third_party/flatbuffers` | `#include`: services ؛ `BUILD.gn`: angle, services ؛ `DEPS`: angle, services | غير مطلوب — يُستخدم فقط في TFLite/WebNN/Optimization Guide غير المطلوبة |
| 50 | `third_party/freetype_buildflags.h` | `#include`: content ؛ `DEPS`: content | غير مطلوب كتنزيل — ملف رأس يُولّد وقت البناء بواسطة GN وليس مستودعاً |
| 51 | `third_party/fuchsia-gn-sdk` | `BUILD.gn`: base, content ؛ `DEPS`: v8 | غير مطلوب — خاص بمنصة Fuchsia غير المدعومة (الخطوة 8) |
| 52 | `third_party/fuchsia-sdk` | `BUILD.gn`: angle, base, cc, content, gpu, mojo, net, services, v8, viz ؛ `DEPS`: angle, v8 | غير مطلوب — خاص بمنصة Fuchsia غير المدعومة (الخطوة 8) |
| 53 | `third_party/fuzztest` | `#include`: base, blink, cc, content, net, services, skia, v8 ؛ `BUILD.gn`: base, blink, content, net, services, v8 ؛ `DEPS`: base, blink, cc, content, net, services, v8 | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 54 | `third_party/gles1_conform` | `DEPS`: angle | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 55 | `third_party/glslang` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 56 | `third_party/google-truth` | `BUILD.gn`: base, content, net, services | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 57 | `third_party/google_benchmark` | `#include`: base, net, services, url ؛ `BUILD.gn`: base, net, services, url, v8 | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 58 | `third_party/google_benchmark_chrome` | `BUILD.gn`: v8 ؛ `DEPS`: v8 | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 59 | `third_party/googletest` | `#include`: angle, blink, net, v8 ؛ `BUILD.gn`: angle, blink, skia, v8 ؛ `DEPS`: angle, net, v8 | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 60 | `third_party/googletest.` | `BUILD.gn`: v8 | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 61 | `third_party/gperf` | `BUILD.gn`: blink | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 62 | `third_party/hamcrest` | `BUILD.gn`: base, content, services | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 63 | `third_party/hyphen` | `DEPS`: content | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 64 | `third_party/hyphenation-patterns` | `BUILD.gn`: blink | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 65 | `third_party/icu4x` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 66 | `third_party/icu_bidi` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 67 | `third_party/ijar` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 68 | `third_party/imgui` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 69 | `third_party/inspector_protocol` | `#include`: blink, content ؛ `BUILD.gn`: blink, content, viz ؛ `DEPS`: blink, content, v8 | غير مطلوب — DevTools وبروتوكول الفحص ممنوعان صراحةً (الخطوة 8) |
| 70 | `third_party/instrumented_libs` | `BUILD.gn`: v8 ؛ `DEPS`: v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 71 | `third_party/ittapi` | `#include`: v8 ؛ `BUILD.gn`: v8 ؛ `DEPS`: v8 | غير مطلوب — واجهة فحص أداء Intel VTune الاختيارية (`checkout_ittapi = False`) |
| 72 | `third_party/jdk` | `BUILD.gn`: base, url ؛ `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 73 | `third_party/jinja2` | `BUILD.gn`: angle, blink, mojo ؛ `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 74 | `third_party/jni_zero` | `#include`: base, content, mojo, services, url ؛ `BUILD.gn`: base, cc, content, gpu, mojo, net, services, url, viz ؛ `DEPS`: base, content, url | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 75 | `third_party/jsoncpp` | `BUILD.gn`: angle, v8 ؛ `DEPS`: angle, v8 | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 76 | `third_party/junit` | `BUILD.gn`: base, content, mojo, net, services, url | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 77 | `third_party/libFuzzer` | `DEPS`: viz | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 78 | `third_party/libavif` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 79 | `third_party/libc` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 80 | `third_party/libgrapheme` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 81 | `third_party/libjingle_xmpp` | `BUILD.gn`: angle | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 82 | `third_party/libjxl` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 83 | `third_party/libpfm4` | `DEPS`: v8 | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 84 | `third_party/libphonenumber` | `BUILD.gn`: content, services | غير مطلوب — خاص بالملء التلقائي (Autofill) الممنوع (الخطوة 8) |
| 85 | `third_party/libprotobuf-mutator` | `#include`: blink, content, gpu, net, services, viz ؛ `BUILD.gn`: base, blink, content, gpu, mojo, net, services ؛ `DEPS`: content, gpu, net, services, viz | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 86 | `third_party/libunwind` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 87 | `third_party/libunwindstack` | `#include`: base ؛ `BUILD.gn`: base ؛ `DEPS`: base | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 88 | `third_party/libusb` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — ميزة WebUSB/USB ممنوعة صراحةً (الخطوة 8) |
| 89 | `third_party/lit` | `BUILD.gn`: content | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 90 | `third_party/litert` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — وقت تشغيل WebNN/LiteRT خارج الميزات المسموحة (الخطوة 6) |
| 91 | `third_party/llvm` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 92 | `third_party/llvm-build` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 93 | `third_party/llvm-libclang` | `BUILD.gn`: v8 ؛ `DEPS`: v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 94 | `third_party/logdog` | `BUILD.gn`: angle ؛ `DEPS`: v8 | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 95 | `third_party/lunarg-vulkantools` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 96 | `third_party/markupsafe` | `BUILD.gn`: mojo ؛ `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 97 | `third_party/material_web_components` | `BUILD.gn`: content | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 98 | `third_party/mesa` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 99 | `third_party/meson` | `DEPS`: angle | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 100 | `third_party/metrics_proto` | `#include`: services ؛ `BUILD.gn`: content, services ؛ `DEPS`: services | غير مطلوب — تتبع القياسات (Telemetry/Metrics/UKM) ممنوع (الخطوة 8) |
| 101 | `third_party/microsoft_webauthn` | `#include`: content ؛ `BUILD.gn`: content ؛ `DEPS`: content | غير مطلوب — ميزة WebAuthn/Credentials ممنوعة صراحةً (الخطوة 8) |
| 102 | `third_party/minigbm` | `BUILD.gn`: angle | غير مطلوب — خاص بمنصة ChromeOS غير المدعومة (الخطوة 8) |
| 103 | `third_party/mockito` | `BUILD.gn`: base, content, net, services, url | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 104 | `third_party/mozilla` | `DEPS`: content | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 105 | `third_party/native_app_glue` | `BUILD.gn`: skia | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 106 | `third_party/ninja` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 107 | `third_party/node` | `BUILD.gn`: blink, content, mojo | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 108 | `third_party/nss` | `DEPS`: net | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 109 | `third_party/nvml` | `DEPS`: gpu | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 110 | `third_party/ocmock` | `#include`: services ؛ `BUILD.gn`: content, services ؛ `DEPS`: content, services | غير مطلوب — أداة اختبارات iOS/macOS (تُحذف مع الاختبارات ومنصة iOS في الخطوة 8) |
| 111 | `third_party/openh264` | `BUILD.gn`: blink ؛ `DEPS`: blink | غير مطلوب — مخصص لترميز WebRTC/RTC فقط |
| 112 | `third_party/openxr` | `BUILD.gn`: content | غير مطلوب — ميزة WebXR ممنوعة صراحةً (الخطوة 8) |
| 113 | `third_party/piex` | `BUILD.gn`: skia | غير مطلوب — اعتماديات اختيارية لبناء Skia المستقل خارج Chromium |
| 114 | `third_party/ply` | `BUILD.gn`: mojo | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 115 | `third_party/pthreadpool` | `BUILD.gn`: services | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 116 | `third_party/pyjson5` | `BUILD.gn`: blink | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 117 | `third_party/pywebsocket3` | `BUILD.gn`: content, services | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 118 | `third_party/quic_trace` | `BUILD.gn`: net | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 119 | `third_party/r8` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 120 | `third_party/rapidjson` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 121 | `third_party/renderdoc` | `#include`: angle | غير مطلوب — أداة فحص وتصحيح الإطارات الرسومية (اختبارات/تصحيح ANGLE) |
| 122 | `third_party/requests` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 123 | `third_party/rust-toolchain` | `BUILD.gn`: angle ؛ `DEPS`: v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 124 | `third_party/sentencepiece` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — ترميز نصوص نماذج الترجمة/TFLite الممنوعة (الخطوة 8) |
| 125 | `third_party/siso` | `DEPS`: angle, v8 | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 126 | `third_party/six` | `DEPS`: angle | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 127 | `third_party/smhasher` | `DEPS`: gpu, services | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 128 | `third_party/speech-dispatcher` | `#include`: content ؛ `BUILD.gn`: content ؛ `DEPS`: content | غير مطلوب — نطق النظام/قارئ الشاشة خارج نطاق بيئة تشغيل الويب |
| 129 | `third_party/spirv-cross` | `BUILD.gn`: skia ؛ `DEPS`: angle | غير مطلوب — خاص بمنصة ChromeOS غير المدعومة (الخطوة 8) |
| 130 | `third_party/spirv-tools` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 131 | `third_party/tensorflow-text` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — تابع لنماذج الترجمة/TFLite الممنوعة (الخطوة 8) |
| 132 | `third_party/test_fonts` | `#include`: base, content ؛ `BUILD.gn`: base ؛ `DEPS`: base, content | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 133 | `third_party/text-fragments-polyfill` | `BUILD.gn`: blink | غير مطلوب — خاص بمشاركة الروابط وتصفح المواقع |
| 134 | `third_party/tflite` | `#include`: content, services ؛ `BUILD.gn`: content, services ؛ `DEPS`: content, services | غير مطلوب — نماذج التعلم الآلي والترجمة (Translate/WebNN) غير مطلوبة وممنوعة (الخطوة 8) |
| 135 | `third_party/tflite_support` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — تابع لـ TFLite/الترجمة والتصنيف غير المطلوب |
| 136 | `third_party/turbine` | `DEPS`: angle | غير مطلوب — خاص بمنصة Android غير المدعومة (الخطوة 8) |
| 137 | `third_party/usb_ids` | `BUILD.gn`: services | غير مطلوب — معرفات USB غير لازمة مع حذف USB (الخطوة 8) |
| 138 | `third_party/utf` | `BUILD.gn`: services | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 139 | `third_party/v8-perf` | `DEPS`: v8 | غير مطلوب — اعتمادية فرعية/اختيارية غير مستخدمة في الجذور المسموحة لتشغيل تطبيقات الويب |
| 140 | `third_party/vulkan-deps` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 141 | `third_party/vulkan-loader` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 142 | `third_party/vulkan-tools` | `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 143 | `third_party/vulkan-utility-libraries` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — أدوات بناء/توليد خارجية (ممنوع GN/Ninja/depot_tools) |
| 144 | `third_party/vulkan-validation-layers` | `BUILD.gn`: angle ؛ `DEPS`: angle | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 145 | `third_party/webgl` | `BUILD.gn`: content | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 146 | `third_party/webrtc` | `#include`: blink, content, services ؛ `BUILD.gn`: angle, blink, content ؛ `DEPS`: content, services | غير مطلوب — ميزة WebRTC ممنوعة صراحةً (الخطوة 8) |
| 147 | `third_party/webrtc_overrides` | `#include`: blink, content ؛ `BUILD.gn`: blink, content, services ؛ `DEPS`: content | غير مطلوب — ميزة WebRTC ممنوعة صراحةً (الخطوة 8) |
| 148 | `third_party/widevine` | `BUILD.gn`: content | غير مطلوب — إدارة الحقوق الرقمية التجارية غير مطلوبة |
| 149 | `third_party/windows_app_sdk_headers` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — خاص بـ Windows ML / WebNN غير المطلوب |
| 150 | `third_party/wpt_tools` | `BUILD.gn`: blink | غير مطلوب — خاص بالاختبارات أو الـ fuzzers أو قياس الأداء الممنوعة (الخطوة 8) |
| 151 | `third_party/wtl` | `BUILD.gn`: content | غير مطلوب — إضافات/أدوات بناء أو اختبارات اختيارية في ANGLE خارج مسار GL/WebGL الأساسي |
| 152 | `third_party/xnnpack` | `#include`: services ؛ `BUILD.gn`: services ؛ `DEPS`: services | غير مطلوب — مسرع TFLite/WebNN غير مطلوب |
| 153 | `third_party/zoslib` | `BUILD.gn`: v8 ؛ `DEPS`: v8 | غير مطلوب — خاص بمنصة z/OS غير المدعومة |
