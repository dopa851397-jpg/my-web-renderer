# BUILD_SYSTEM_REMOVAL.md — إزالة منظومة بناء Chromium بالكامل

> المرحلة الثالثة (شرط أساسي غير قابل للتفاوض). **لم تُنفّذ أي عملية Build أو Compile، ولم يُنشأ نظام بناء بديل.**

## 1. ما أُزيل

| الفئة | العدد | الوصف |
|---|---:|---|
| `gn_gyp` | 1,069 | كل `BUILD.gn` (763) و`*.gni` (305) و`.gn` (1) — تعريفات الأهداف والإعدادات |
| `gclient_deps` | 503 | كل قوائم `DEPS` (manifests الخاصة بـ gclient/depot_tools) |
| `chromium_infra` | 909 | `OWNERS` (555)، `DIR_METADATA` (302)، `PRESUBMIT.py` (17)، `COMMON_METADATA`، `codereview.settings`، `WATCHLISTS`، `vpython.toml` — بنية حوكمة مشروع Chromium |
| `build_dir` | 78 | إعدادات/sكربتات `build/` (config/, toolchain/, win/, apple/, linux/, mac/, util/, rust/*.gni, gni_impl/) |
| `gn_helpers` | 11 | مجلدات `build_overrides/` و`gni/` و`gn/` (skia/gn, angle/gni, v8/gni, perfetto/gn, partition_allocator/gn) |
| `chromium_codegen` | 389 | مولّدات الكود وقت البناء التي يستدعيها GN: `blink/renderer/build/scripts`, `blink/renderer/bindings/scripts`, `mojo/public/tools/{mojom,bindings}`, `v8/tools/metagen`, `gpu/command_buffer/build_cmd_buffer_lib.py` |
| `build_scripts` | 4 | سكربتات FFmpeg robo التي تستدعي GN/Ninja/depot_tools |
| **الإجمالي** | **2,963** | **11.26 MB** |

### أدوات بحث عنها وتأكد غيابها
- **GN**: لا يوجد أي `BUILD.gn`/`*.gni`/`.gn` (تحقق: `find … = 0`).
- **Ninja**: لا توجد ملفات `*.ninja` ولا ثنائي ninja. (ملاحظة: `third_party/perfetto/src/trace_processor/importers/ninja` هو **كود مصدري** لمستورد سجلات ninja في Perfetto وليس أداة البناء — أُبقي عليه.)
- **GYP**: لا `*.gyp`/`*.gypi`.
- **gclient / depot_tools / autoninja / mb.py**: لا توجد ملفات `.gclient*` ولا `autoninja*` ولا `mb.py` ولا مجلد `depot_tools`.
- **استدعاءات متبقية**: فحص `grep -rlE 'autoninja|gclient |depot_tools|gn gen|ninja -C|mb\.py'` على كل `*.py/*.sh/*.bat/*.ps1` = **0**.

## 2. ما أُبقي عليه داخل `build/` (رؤوس مصدرية بحتة — ليست أدوات بناء)

هذه ملفات C/C++/Rust مصدرية تُضمّن مباشرة من الكود ولا يمكن حذفها دون كسر آلاف الملفات:

| الملف | السبب |
|---|---|
| `build/build_config.h` | مضمّن في **2,334** ملفاً (ماكروهات OS/CPU/compiler) |
| `build/buildflag.h` | مضمّن في 55 ملفاً (ماكرو BUILDFLAG) |
| `build/sanitizers/*.{h,cc,c}` | كود دعم Sanitizers مصدري (تصحيح أساسي) |
| `build/rust/allocator/*.{h,cc,rs}` | كود Rust/C++ لمخصّص الذاكرة |
| `build/rust/chromium_prelude/*.rs` | كود Rust مصدري |

> ملاحظة: `compiler_specific.h` انتقل upstream إلى `base/compiler_specific.h` وهو موجود. الرؤوس المولّدة مثل `build/*_buildflags.h` تُنتج وقت البناء oleh نظام البناء المستقبلي (غير موجودة في المصدر الخام — طبيعي).

## 3. البيانات المصدرية التي أُبقي عليها (ليست اعتماديات بناء فعلية)

- **`.mojom` (880+)** و**`.idl` (1,372+)** و**`.json5`**: تعريفات واجهات الويب وMojo — بيانات مصدرية تُحوّلها مولّدات الكود. أُبقي عليها لأنها المصدر الحقيقي لواجهات Web Platform.
- **قوالب Dawn** (`third_party/dawn/generator/`): قوالب codegen مصدرية.
- **`.grd`**: تعريفات موارد (بيانات).
- **أرشيف DEPS الأصلي**: نُقل إلى `docs/provenance/chromium-158.0.8127.89.DEPS.txt` كسجل تاريخي للإصدارات المثبّتة (ليس manifest نشطاً لـ gclient).

## 4. القرار المعماري بخصوص مولّدات الكود

مولّداتBindings/IDL/mojom هي أدوات بناء Chromium خاصة تستدعى من GN. بموجب شرط «إزالة منظومة بناء Chromium بالكامل» أُزيلت، مع **الإبقاء على بيانات الـ IDL/mojom/json5 والقوالب**. نظام البناء المستقبلي المستقل (Ultra Desktop Framework) سيوفّر تكامل codegen الخاص به أو يعيد جلب هذه المولّدات من upstream عند الحاجة. هذا موثّق وقابل للعكس.

## 5. التحقق النهائي

```
find . -name BUILD.gn -o -name '*.gni' -o -name '.gn' -o -name DEPS -o -name '.gclient*'  → 0
grep -rlE 'autoninja|gclient |depot_tools|gn gen|ninja -C' --include='*.py' …            → 0
```

**النتيجة: منظومة بناء Chromium (GN/Ninja/GYP/gclient/depot_tools/autoninja) أُزيلت بالكامل من الشجرة، مع الحفاظ على الرؤوس المصدرية الضرورية وبيانات الواجهات.**
