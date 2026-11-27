# REMOVED_FILES.md — سجل الملفات والمجلدات المحذوفة وأسبابها

> إجمالي المحذوف في هذه المهمة: **4,914 ملفاً** (53.17 MB) + 10 رابطاً رمزياً مكسوراً. لا يشمل حذف التقليم السابق (339,051 ملفاً في REMOVED.txt). السجلات الخام في [`docs/logs/`](docs/logs/).

## ملخص حسب الفئة

| الفئة | العدد | السبب |
|---|---:|---|
| `build_dir` | 78 | إعدادات/سكربتات build/ |
| `build_scripts` | 4 | سكربتات تستدعي GN/Ninja/depot_tools |
| `chromium_codegen` | 389 | مولّدات كود Chromium وقت البناء |
| `chromium_infra` | 909 | بيانات حوكمة مشروع Chromium |
| `cleanup` | 1,941 | اختبارات/fuzzers/ربط Node.js/أجزاء ML اختيارية/بيانات اختبار/تنفيذيات |
| `gclient_deps` | 503 | قوائم gclient (DEPS) |
| `gn_gyp` | 1,069 | تعريفات بناء GN/GYP |
| `gn_helpers` | 11 | مجلدات مساعدات GN |
| روابط رمزية مكسورة | 10 | مراجع مكسورة لملفات محذوفة سابقاً |

## عينة تفصيلية (أول 40 مساراً لكل فئة)

### build_dir (78)

- `/home/user/my-web-renderer/build/zip_helpers.py`
- `/home/user/my-web-renderer/build/vs_toolchain.py`
- `/home/user/my-web-renderer/build/noop.py`
- `/home/user/my-web-renderer/build/protoc_java.py`
- `/home/user/my-web-renderer/build/write_buildflag_header.py`
- `/home/user/my-web-renderer/build/precompile.cc`
- `/home/user/my-web-renderer/build/compute_build_timestamp.py`
- `/home/user/my-web-renderer/build/gn_helpers.py`
- `/home/user/my-web-renderer/build/gn_run_binary.py`
- `/home/user/my-web-renderer/build/metadata.json.in`
- `/home/user/my-web-renderer/build/precompile.h`
- `/home/user/my-web-renderer/build/action_helpers.py`
- `/home/user/my-web-renderer/build/config/compiler_cpu_abi.gn`
- `/home/user/my-web-renderer/build/config/c++/libc++.natvis`
- `/home/user/my-web-renderer/build/config/linux/pkg-config.py`
- `/home/user/my-web-renderer/build/config/linux/cached_results.scope`
- `/home/user/my-web-renderer/build/config/apple/codesign.py`
- `/home/user/my-web-renderer/build/config/apple/sdk_info.py`
- `/home/user/my-web-renderer/build/config/apple/cxx_imports_apinotes.py`
- `/home/user/my-web-renderer/build/config/apple/compile_ib_files.py`
- `/home/user/my-web-renderer/build/config/apple/cxx_imports.modulemap.jinja`
- `/home/user/my-web-renderer/build/config/apple/find_signing_identity.py`
- `/home/user/my-web-renderer/build/config/apple/write_framework_hmap.py`
- `/home/user/my-web-renderer/build/config/apple/write_framework_modulemap.py`
- `/home/user/my-web-renderer/build/config/tvos/BuildInfo.plist`
- `/home/user/my-web-renderer/build/config/sanitizers/ignorelist_stdlib_and_absl.txt`
- `/home/user/my-web-renderer/build/config/mac/BuildInfo.plist`
- `/home/user/my-web-renderer/build/config/mac/prepare_framework_version.py`
- `/home/user/my-web-renderer/build/config/mac/package_framework.py`
- `/home/user/my-web-renderer/build/util/LASTCHANGE.dummy`
- `/home/user/my-web-renderer/build/util/chromium_git_revision.h.in`
- `/home/user/my-web-renderer/build/util/version.py`
- `/home/user/my-web-renderer/build/util/generate_wrapper.py`
- `/home/user/my-web-renderer/build/util/MINIBRANCH.dummy`
- `/home/user/my-web-renderer/build/util/lib/__init__.py`
- `/home/user/my-web-renderer/build/win/use_ansi_codes.py`
- `/home/user/my-web-renderer/build/win/segment_heap.manifest`
- `/home/user/my-web-renderer/build/win/compatibility.manifest`
- `/home/user/my-web-renderer/build/win/as_invoker.manifest`
- `/home/user/my-web-renderer/build/win/set_appcontainer_acls.py`
- … و38 مساراً آخر (القائمة الكاملة في `docs/logs/`)

### build_scripts (4)

- `/home/user/my-web-renderer/media/ffmpeg/scripts/robo_build.py`
- `/home/user/my-web-renderer/media/ffmpeg/scripts/robo_setup.py`
- `/home/user/my-web-renderer/media/ffmpeg/scripts/robo_lib/config.py`
- `/home/user/my-web-renderer/media/ffmpeg/scripts/win_env.sh`

### chromium_codegen (389)

- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_settings.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_element_factory.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/generate_permission_element_grd.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_element_type_enum.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/aria_properties.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_policy_helper.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_element_lookup_trie.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_runtime_features_utilities.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_common_features.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_document_policy_features_util.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/license.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_element_attribute_name_lookup_trie.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_html_entity_table.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_element_type_helpers.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_document_policy_features.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_runtime_features.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_deprecation_info.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_runtime_feature_state_override_context.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_names.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_runtime_feature_mojom_defs.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/gperf.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_style_builder.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_runtime_feature_state_contexts_headers.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/media_feature_symbol.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_runtime_feature_state_contexts_impl.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_ax_utilities.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_web_origin_trials.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_origin_trial_feature_mojom_defs.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_origin_trials.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_event_factory.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_qualified_names.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_policy_helper_public.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/template_expander.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_runtime_features_for_public.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/keyword_utils.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/make_instrumenting_probes.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/run_with_pythonpath.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/blinkbuild/__init__.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/blinkbuild/name_style_converter.py`
- `/home/user/my-web-renderer/blink/renderer/build/scripts/templates/document_policy_features.cc.tmpl`
- … و349 مساراً آخر (القائمة الكاملة في `docs/logs/`)

### chromium_infra (909)

- `/home/user/my-web-renderer/gpu/GLES2/OWNERS`
- `/home/user/my-web-renderer/gpu/config/PRESUBMIT.py`
- `/home/user/my-web-renderer/gpu/config/OWNERS`
- `/home/user/my-web-renderer/gpu/ipc/client/OWNERS`
- `/home/user/my-web-renderer/gpu/ipc/service/OWNERS`
- `/home/user/my-web-renderer/gpu/ipc/common/PRESUBMIT.py`
- `/home/user/my-web-renderer/gpu/ipc/common/OWNERS`
- `/home/user/my-web-renderer/gpu/vulkan/PRESUBMIT.py`
- `/home/user/my-web-renderer/gpu/vulkan/OWNERS`
- `/home/user/my-web-renderer/gpu/command_buffer/PRESUBMIT.py`
- `/home/user/my-web-renderer/gpu/command_buffer/OWNERS`
- `/home/user/my-web-renderer/gpu/command_buffer/client/internal/OWNERS`
- `/home/user/my-web-renderer/angle/src/compiler/translator/OWNERS`
- `/home/user/my-web-renderer/angle/src/libANGLE/renderer/wgpu/OWNERS`
- `/home/user/my-web-renderer/angle/src/libANGLE/renderer/gl/OWNERS`
- `/home/user/my-web-renderer/angle/src/libANGLE/renderer/metal/OWNERS`
- `/home/user/my-web-renderer/angle/src/libANGLE/renderer/vulkan/OWNERS`
- `/home/user/my-web-renderer/angle/src/libANGLE/renderer/d3d/OWNERS`
- `/home/user/my-web-renderer/angle/src/common/base/anglebase/numerics/OWNERS`
- `/home/user/my-web-renderer/blink/public/platform/OWNERS`
- `/home/user/my-web-renderer/blink/public/platform/media/OWNERS`
- `/home/user/my-web-renderer/blink/public/platform/media/DIR_METADATA`
- `/home/user/my-web-renderer/blink/public/platform/audio/OWNERS`
- `/home/user/my-web-renderer/blink/public/platform/audio/DIR_METADATA`
- `/home/user/my-web-renderer/blink/public/platform/scheduler/OWNERS`
- `/home/user/my-web-renderer/blink/public/platform/scheduler/DIR_METADATA`
- `/home/user/my-web-renderer/blink/public/platform/modules/service_worker/OWNERS`
- `/home/user/my-web-renderer/blink/public/platform/modules/service_worker/DIR_METADATA`
- `/home/user/my-web-renderer/blink/public/mojom/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/associated_interfaces/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/call_stack_generator/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/service_worker/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/service_worker/DIR_METADATA`
- `/home/user/my-web-renderer/blink/public/mojom/device/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/font_unique_name_lookup/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/leak_detector/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/leak_detector/DIR_METADATA`
- `/home/user/my-web-renderer/blink/public/mojom/window_features/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/gpu/OWNERS`
- `/home/user/my-web-renderer/blink/public/mojom/webpreferences/OWNERS`
- … و869 مساراً آخر (القائمة الكاملة في `docs/logs/`)

### cleanup (1,941)

- `third_party/dawn/src/dawn/node/NapiSymbols.cpp`
- `third_party/dawn/src/dawn/node/README.md`
- `third_party/dawn/src/dawn/node/ManualConstructors.h`
- `third_party/dawn/src/dawn/node/Module.cpp`
- `third_party/dawn/src/dawn/node/ManualConstructors.cpp`
- `third_party/dawn/src/dawn/node/index.js`
- `third_party/dawn/src/dawn/node/worker-test.mjs`
- `third_party/dawn/src/dawn/node/Module.h`
- `third_party/dawn/src/dawn/node/test.mjs`
- `third_party/dawn/src/dawn/node/gen_napi_symbols.py`
- `third_party/dawn/src/dawn/node/cts.cjs`
- `third_party/dawn/src/dawn/node/interop/DawnExtensions.idl`
- `third_party/dawn/src/dawn/node/interop/WebGPU.h.tmpl`
- `third_party/dawn/src/dawn/node/interop/WebGPUCommon.tmpl`
- `third_party/dawn/src/dawn/node/interop/Core.h`
- `third_party/dawn/src/dawn/node/interop/Browser.idl`
- `third_party/dawn/src/dawn/node/interop/WebGPU.cpp.tmpl`
- `third_party/dawn/src/dawn/node/interop/Core.cpp`
- `third_party/dawn/src/dawn/node/interop/NodeAPI.h`
- `third_party/dawn/src/dawn/node/binding/GPUBindGroupLayout.h`
- `third_party/dawn/src/dawn/node/binding/GPUCommandBuffer.cpp`
- `third_party/dawn/src/dawn/node/binding/GPUResourceTable.h`
- `third_party/dawn/src/dawn/node/binding/IteratorHelper.h`
- `third_party/dawn/src/dawn/node/binding/GPUQueue.h`
- `third_party/dawn/src/dawn/node/binding/GPUAdapter.h`
- `third_party/dawn/src/dawn/node/binding/Split.h`
- `third_party/dawn/src/dawn/node/binding/GPUQuerySet.cpp`
- `third_party/dawn/src/dawn/node/binding/Converter.h`
- `third_party/dawn/src/dawn/node/binding/GPUSampler.cpp`
- `third_party/dawn/src/dawn/node/binding/TogglesLoader.h`
- `third_party/dawn/src/dawn/node/binding/GPUDevice.h`
- `third_party/dawn/src/dawn/node/binding/GPURenderBundleEncoder.h`
- `third_party/dawn/src/dawn/node/binding/GPUTextureView.cpp`
- `third_party/dawn/src/dawn/node/binding/GPUComputePassEncoder.h`
- `third_party/dawn/src/dawn/node/binding/GPUSupportedLimits.h`
- `third_party/dawn/src/dawn/node/binding/GPURenderPassEncoder.h`
- `third_party/dawn/src/dawn/node/binding/GPUAdapter.cpp`
- `third_party/dawn/src/dawn/node/binding/GPUQuerySet.h`
- `third_party/dawn/src/dawn/node/binding/GPUPipelineLayout.h`
- `third_party/dawn/src/dawn/node/binding/GPUTexture.cpp`
- … و1,901 مساراً آخر (القائمة الكاملة في `docs/logs/`)

### gclient_deps (503)

- `/home/user/my-web-renderer/device/base/DEPS`
- `/home/user/my-web-renderer/gpu/DEPS`
- `/home/user/my-web-renderer/gpu/config/DEPS`
- `/home/user/my-web-renderer/gpu/ipc/DEPS`
- `/home/user/my-web-renderer/gpu/ipc/host/DEPS`
- `/home/user/my-web-renderer/gpu/ipc/client/DEPS`
- `/home/user/my-web-renderer/gpu/ipc/service/DEPS`
- `/home/user/my-web-renderer/gpu/ipc/common/DEPS`
- `/home/user/my-web-renderer/gpu/vulkan/DEPS`
- `/home/user/my-web-renderer/gpu/command_buffer/client/DEPS`
- `/home/user/my-web-renderer/gpu/command_buffer/client/internal/DEPS`
- `/home/user/my-web-renderer/gpu/command_buffer/service/DEPS`
- `/home/user/my-web-renderer/gpu/command_buffer/service/shared_image/DEPS`
- `/home/user/my-web-renderer/gpu/command_buffer/common/DEPS`
- `/home/user/my-web-renderer/build/DEPS`
- `/home/user/my-web-renderer/build/rust/DEPS`
- `/home/user/my-web-renderer/build/rust/allocator/DEPS`
- `/home/user/my-web-renderer/gin/DEPS`
- `/home/user/my-web-renderer/ipc/DEPS`
- `/home/user/my-web-renderer/sandbox/DEPS`
- `/home/user/my-web-renderer/sandbox/linux/DEPS`
- `/home/user/my-web-renderer/sandbox/linux/seccomp-bpf/DEPS`
- `/home/user/my-web-renderer/sandbox/linux/bpf_dsl/DEPS`
- `/home/user/my-web-renderer/sandbox/linux/seccomp-bpf-helpers/DEPS`
- `/home/user/my-web-renderer/sandbox/linux/suid/client/DEPS`
- `/home/user/my-web-renderer/sandbox/linux/syscall_broker/DEPS`
- `/home/user/my-web-renderer/sandbox/linux/services/DEPS`
- `/home/user/my-web-renderer/sandbox/policy/DEPS`
- `/home/user/my-web-renderer/sandbox/policy/mac/DEPS`
- `/home/user/my-web-renderer/sandbox/mac/DEPS`
- `/home/user/my-web-renderer/sandbox/mac/mojom/DEPS`
- `/home/user/my-web-renderer/blink/public/DEPS`
- `/home/user/my-web-renderer/blink/public/platform/DEPS`
- `/home/user/my-web-renderer/blink/public/platform/win/DEPS`
- `/home/user/my-web-renderer/blink/public/platform/media/DEPS`
- `/home/user/my-web-renderer/blink/public/platform/scheduler/DEPS`
- `/home/user/my-web-renderer/blink/public/mojom/DEPS`
- `/home/user/my-web-renderer/blink/public/common/DEPS`
- `/home/user/my-web-renderer/blink/public/common/link_to_text/DEPS`
- `/home/user/my-web-renderer/blink/public/common/renderer_preferences/DEPS`
- … و463 مساراً آخر (القائمة الكاملة في `docs/logs/`)

### gn_gyp (1,069)

- `/home/user/my-web-renderer/device/base/BUILD.gn`
- `/home/user/my-web-renderer/device/base/public/cpp/BUILD.gn`
- `/home/user/my-web-renderer/device/base/synchronization/BUILD.gn`
- `/home/user/my-web-renderer/device/udev_linux/BUILD.gn`
- `/home/user/my-web-renderer/gpu/BUILD.gn`
- `/home/user/my-web-renderer/gpu/config/BUILD.gn`
- `/home/user/my-web-renderer/gpu/ipc/BUILD.gn`
- `/home/user/my-web-renderer/gpu/ipc/host/BUILD.gn`
- `/home/user/my-web-renderer/gpu/ipc/client/BUILD.gn`
- `/home/user/my-web-renderer/gpu/ipc/service/BUILD.gn`
- `/home/user/my-web-renderer/gpu/ipc/common/BUILD.gn`
- `/home/user/my-web-renderer/gpu/ipc/common/generated_vulkan_type_mappings.gni`
- `/home/user/my-web-renderer/gpu/vulkan/features.gni`
- `/home/user/my-web-renderer/gpu/vulkan/BUILD.gn`
- `/home/user/my-web-renderer/gpu/vulkan/init/BUILD.gn`
- `/home/user/my-web-renderer/gpu/vulkan/win32/BUILD.gn`
- `/home/user/my-web-renderer/gpu/vulkan/mac/BUILD.gn`
- `/home/user/my-web-renderer/gpu/command_buffer/client/BUILD.gn`
- `/home/user/my-web-renderer/gpu/command_buffer/client/internal/BUILD.gn`
- `/home/user/my-web-renderer/gpu/command_buffer/service/BUILD.gn`
- `/home/user/my-web-renderer/gpu/command_buffer/common/BUILD.gn`
- `/home/user/my-web-renderer/build/timestamp.gni`
- `/home/user/my-web-renderer/build/BUILD.gn`
- `/home/user/my-web-renderer/build/nocompile.gni`
- `/home/user/my-web-renderer/build/compiled_action.gni`
- `/home/user/my-web-renderer/build/buildflag_header.gni`
- `/home/user/my-web-renderer/build/gn_logs.gni`
- `/home/user/my-web-renderer/build/linux/BUILD.gn`
- `/home/user/my-web-renderer/build/linux/sysroot_scripts/sysroot.gni`
- `/home/user/my-web-renderer/build/config/locales.gni`
- `/home/user/my-web-renderer/build/config/pch.gni`
- `/home/user/my-web-renderer/build/config/ozone.gni`
- `/home/user/my-web-renderer/build/config/chrome_build.gni`
- `/home/user/my-web-renderer/build/config/dcheck_always_on.gni`
- `/home/user/my-web-renderer/build/config/loongarch64.gni`
- `/home/user/my-web-renderer/build/config/buildflags_paint_preview.gni`
- `/home/user/my-web-renderer/build/config/rts.gni`
- `/home/user/my-web-renderer/build/config/ozone_extra.gni`
- `/home/user/my-web-renderer/build/config/python.gni`
- `/home/user/my-web-renderer/build/config/features.gni`
- … و1,029 مساراً آخر (القائمة الكاملة في `docs/logs/`)

### gn_helpers (11)

- `/home/user/my-web-renderer/base/allocator/partition_allocator/gn/cp.py`
- `/home/user/my-web-renderer/base/allocator/partition_allocator/gn/BUILDCONFIG.gn`
- `/home/user/my-web-renderer/base/allocator/partition_allocator/gn/rm.py`
- `/home/user/my-web-renderer/third_party/perfetto/gn/write_buildflag_header.py`
- `/home/user/my-web-renderer/skia/gn/cp.py`
- `/home/user/my-web-renderer/skia/gn/minify_sksl.py`
- `/home/user/my-web-renderer/skia/gn/find_headers.py`
- `/home/user/my-web-renderer/skia/gn/rm.py`
- `/home/user/my-web-renderer/skia/gn/run_sksllex.py`
- `/home/user/my-web-renderer/skia/gn/bazel_build.py`
- `/home/user/my-web-renderer/skia/gn/toolchain/num_cpus.py`

## الروابط الرمزية المكسورة المحذوفة

- `./third_party/swiftshader/third_party/subzero/DESIGN.rst` → `docs/DESIGN.rst`
- `./third_party/libxslt/linux/COPYING` → `../src/Copyright`
- `./third_party/perfetto/tools/check_imports` → `shim`
- `./third_party/perfetto/tools/roll_syntaqlite` → `shim`
- `./third_party/perfetto/tools/check_trace_processor_deps` → `shim`
- `./third_party/perfetto/tools/check_ratchet` → `shim`
- `./third_party/perfetto/tools/roll_emscripten` → `shim`
- `./third_party/perfetto/tools/roll_node` → `shim`
- `./third_party/wayland/src/git-blame-ignore-revs` → `.git-blame-ignore-revs`
- `./skia/src/ports/fontations/Cargo.toml` → `../../../bazel/external/fontations/Cargo.toml`

> لم يُحذف أي ملف ترخيص فعلي؛ أُعيد ترخيص libxslt `Copyright` المفقود من خط الأساس.