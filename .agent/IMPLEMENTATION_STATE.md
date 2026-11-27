# IMPLEMENTATION_STATE.md — current checkpoint (2026-11-27)

Older detail lives in `archive/`. Rules: `ENGINEERING_RULES.md`. Per-feature statuses: `implementation.md`.

## Baselines and branches
- Template source: `Flutter-App-Template`, branch `feat/template-v2`, commit `062e620` (caller pins Gateway `v1.1.0`, which resolves to gateway commit `635b040`).
- Default branch `main` of this repo: `062e620` = the template commit, unchanged. Never owner-confirmed on a device (throw-away repo).
- Working branch `agent/e2e`: code commit `8af143d` (rename + notifications feature + plugin deps + initial `.agent/`), CI-green, not device-tested, not merged. A later docs-only commit `docs: bootstrap .agent` sits on top; its own CI run is recorded in the Build log once finished.
- Rollback: `main` (`062e620`) is the clean template; PR #1 is not merged.

## This session (2026-11-27)
- Changed (and why): `.agent/` memory only (BRIEF, HANDOFF, IMPLEMENTATION_STATE, CHANGELOG, implementation.md): the bootstrap files still held template placeholders. No code, workflow or template change.
- Verified — and HOW:
  - PR #1 open, head `8af143d`, base `main`, clean; GitHub Actions run 45966298363 (pull_request) for that exact head: `android / Build APK (release)` success, `method / Agent memory audit` success (CI).
  - Inside the APK job every step succeeded, including Analyze, Test (annotation says `analyze=ran tests=ran`, so `widget_test.dart` was part of the run) and Build APK (CI). Test counts are not readable: job-log download is blocked from the sandbox.
  - CI annotation reports `package=com.example.tpl_e2e`, APK 43M, apk_sha256 `2ae75ba806c65879fae137240e7e674d0a1181933373fa54dea67b2b983e90e0`, signer_sha256 `136966601854d1bd1397841d7d5ef10f1145bd8ac71c49f8ac6812857f136233` (the APK file itself was not downloaded here).
  - Rename (read the code): `pubspec.yaml` name `tpl_e2e`; all `package:` imports in `lib/` and `test/` updated; no remaining `app_template` text anywhere outside `.git`; `scaffold_args` is `--org com.example`; `tool/android_label.txt` holds the new label.
  - Resolved dependencies (CI annotation): `shared_preferences` 2.5.6, `shared_preferences_android` 2.5.5, `flutter_local_notifications` 17.2.4, `timezone` 0.9.4.
- NOT verified: the launcher label on a device (contains `&`; `tool/ci_android.sh` escapes it and checks its own result in CI, but the rendered name was not seen); the Android `namespace` (`android/` is generated in CI and not committed, so it was not inspected); the notifications native injection at runtime (no Dart code uses the plugin yet, so the build proves compilation and R8 only); `shared_preferences_android` 2.5.5 on the owner's phone (`docs/RECIPES.md` records a black screen with 2.5.0 on that phone); anything on a device.
- Corrections of earlier wrong claims: the hand-over described the PR as a rename only. Commit `8af143d` also adds the `notifications` feature (`tool/android_features.txt`) and three dependencies (`shared_preferences`, `flutter_local_notifications`, `timezone`). The earlier "2 audit warnings" could not be reproduced on the committed state (local audit: 0 errors, 0 warnings).

## Needs owner device test (not verifiable in CI)
1. Install the APK of run 45966298363 (or a newer green one): launcher name should read `اختبار & القالب`, app opens (no black screen), package `com.example.tpl_e2e`.

## Open items / next (priority order)
1. Owner reviews the report and decides on merging PR #1 (not merged by the agent).
2. Gateway audit finding for the owner: `agent_audit.py` only flags double-angle-bracket upper-case placeholders, so a bootstrap full of `…` / `<text>` placeholders passes with 0 warnings. Not changed here (gateway is out of scope for this test).
3. `ARCHITECTURE.md`, `DECISIONS.md`, `LESSONS.md` still hold template text; fill them only with real content.

## Build log
8af143d rename + notifications + deps + .agent · green (run 45966298363) · not device-tested
