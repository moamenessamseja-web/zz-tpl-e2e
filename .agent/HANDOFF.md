# HANDOFF.md — 60-second start

1. Read `README.md` → `ENGINEERING_RULES.md` → `IMPLEMENTATION_STATE.md`.
2. **Test target now:** branch `agent/e2e`, PR #1 (open, not merged). Last CI-green code commit: `8af143d` (run 45966298363). Last owner-confirmed on a device: none. Distrust: nothing is device-tested; the launcher label, the applicationId on the phone and the `shared_preferences_android` runtime behaviour are unverified on hardware.
3. Owner's current task list: (a) review the E2E report and decide whether the template is ready to merge; (b) fill `BRIEF.md` only if this repo becomes a real app. Status: waiting for the owner.
4. Do not: merge PR #1 or touch `main` before the owner's OK · change the template or the gateway for cosmetic reasons · skip or weaken a failing test · claim device-level results that did not happen · commit secrets.
5. Environment notes: no Flutter SDK in the agent sandbox; verification is GitHub Actions only (CI job logs and artifact download are not reachable from the sandbox, so results are read from check-run annotations). Tokens are given for a session and are never written to the repo.

## Session 2026-11-27
- Resumed the E2E test from its recorded state, re-verified PR #1 and CI against GitHub, reviewed the rename, and filled this memory with real values.
