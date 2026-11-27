# implementation.md — inventory of what exists (honest statuses)

Statuses (use ONLY these, never promote without evidence): **Verified complete** · **Implemented, not yet verified** · **Partially implemented** ·
**Not started** · **Blocked** · **Deferred by product decision**.
Evidence levels: *read* < *sanity* < *CI* < *artifact inspected* < *owner's device*. "Verified complete" needs the owner's device for anything user-facing.

## 1. Template identity (rename)
| Item | Status | Notes (evidence, build, limits) |
|---|---|---|
| Dart package name `tpl_e2e` and `package:` imports | Verified complete | read + CI (analyze and tests ran on 8af143d); no `app_template` text left |
| Android applicationId `com.example.tpl_e2e` | Implemented, not yet verified | CI annotation `package=com.example.tpl_e2e`; APK not inspected here; fixed after the first phone install by design |
| Launcher label `اختبار & القالب` | Implemented, not yet verified | `tool/ci_android.sh` escapes `&` and checks its own result (CI green); not seen on a device |
| Android namespace | Implemented, not yet verified | `android/` is generated in CI, not committed; not inspected |

## 2. Native features and dependencies
| Item | Status | Notes (evidence, build, limits) |
|---|---|---|
| `notifications` native injection (manifest, receivers, R8 rules, desugaring) | Implemented, not yet verified | CI release build green; no Dart code uses the plugin, so no runtime coverage |
| `shared_preferences` ^2.3.0 (resolved 2.5.6, android 2.5.5) | Implemented, not yet verified | per docs/RECIPES.md; RECIPES notes a black screen with android 2.5.0 on the owner's phone; needs a device test |

## 3. Tests and CI
| Item | Status | Notes (evidence, build, limits) |
|---|---|---|
| flutter analyze, flutter test (incl. widget_test.dart), release APK build, method audit | Verified complete | CI run 45966298363 on 8af143d; counts not readable from the sandbox |

## 4. Memory docs
| Item | Status | Notes (evidence, build, limits) |
|---|---|---|
| BRIEF.md | Blocked | waiting for the owner's verbatim brief |
| ARCHITECTURE.md, DECISIONS.md, LESSONS.md | Not started | still template text |

## Verification log
| Build | Commit | CI | Device |
|---|---|---|---|
| run 45966298363 | 8af143d | green (APK + method audit) | not tested |
