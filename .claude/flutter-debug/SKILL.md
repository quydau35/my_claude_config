---
name: flutter-debug
description: Launch, debug, and monitor Flutter apps on emulators/devices. Use when user says "debug the app", "run on emulator", "check for crashes", "flutter debug", "launch the app", or wants to collect debug console output.
---

# Flutter Debug

## Philosophy

**Core principle**: Debug by running real code on real devices. Console output doesn't lie — stack traces tell you exactly what broke and where. Fix bugs at the source, verify with tests, confirm on device.

**Good debugging** is iterative: launch → observe → diagnose → fix → relaunch. Each cycle gives you new information. Don't guess — read the logs.

**Bad debugging** is speculative: reading code and imagining what might go wrong without running it. The emulator is your ground truth.

## Modes

This skill has 6 modes. Determine which the user needs, or run **full cycle** if they just say "debug the app".

| Mode | Trigger | Reference |
|---|---|---|
| Launch & Monitor | "debug the app", "run on emulator" | [launch.md](launch.md) |
| Collect & Analyze Logs | "check the logs", "any errors?" | [logs.md](logs.md) |
| Stop & Restart | "restart the app", "stop it" | [lifecycle.md](lifecycle.md) |
| Screenshot Capture | "take a screenshot", "show me the screen" | [screenshot.md](screenshot.md) |
| Performance Profiling | "why is it slow", "skipped frames" | [performance.md](performance.md) |
| Auto-Diagnose & Fix | "fix the crash", "full debug cycle" | [diagnose.md](diagnose.md) |

## Workflow (Full Cycle)

1. Discover devices → `flutter devices`
2. Run tests → `flutter test` (TDD gate)
3. Launch debug → `flutter run --debug -d <device_id>` (background)
4. Monitor output → check for crashes or success
5. If crash → read [diagnose.md](diagnose.md), fix, re-run tests, relaunch
6. If success → report status, keep monitoring

## Important Rules

- **Always run tests before launching** — catch bugs at unit level first
- **Background process is non-interactive** — no hot reload. Stop and relaunch for code changes.
- **Keep the task ID** — save it so you can check output and stop the process later
- **Clean up** — always stop the background process when debugging is done

See [log-patterns.md](log-patterns.md) for filtering noise from real errors.
