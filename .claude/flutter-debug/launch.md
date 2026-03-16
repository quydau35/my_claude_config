# Launch & Monitor

## Device Discovery

First, find what's connected:

```bash
flutter devices
```

If no device found, check and launch an emulator:

```bash
flutter emulators
flutter emulators --launch <emulator_id>
```

Wait 15-30 seconds for boot, then re-check `flutter devices`.

## TDD Gate

Run tests before launching. Don't ship broken code to device:

```bash
flutter test
```

If tests fail → STOP. Report failures. Do not launch a broken app.
Skip only if user explicitly says "skip tests".

## Launch

Run as a background task so the conversation continues:

```bash
flutter run --debug -d <device_id> 2>&1
```

Use `run_in_background: true`. Save the task ID.

## Verify Startup

Check output after ~15 seconds. Look for:

| Output | Meaning |
|---|---|
| `✓ Built build/app/outputs/flutter-apk/app-debug.apk` | Build OK |
| `Syncing files to device` | Install OK |
| `Flutter run key commands` | App running |
| `EXCEPTION CAUGHT` | Crash — see [diagnose.md](diagnose.md) |
| `Unhandled Exception` | Crash — see [diagnose.md](diagnose.md) |

## Report

- ✅ **Success**: "App launched on [device]. No errors. [N warnings ignored]."
- ❌ **Crash**: Extract error, identify root cause, propose fix.
