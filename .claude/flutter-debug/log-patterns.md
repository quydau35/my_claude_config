# Log Patterns

Quick reference for filtering Flutter debug console output.

## Real Errors — Investigate Immediately

| Pattern                                   | What It Means                                             |
| ----------------------------------------- | --------------------------------------------------------- |
| `E/flutter`                             | Flutter framework error                                   |
| `EXCEPTION CAUGHT BY WIDGETS LIBRARY`   | Widget build failure — broken widget tree                |
| `EXCEPTION CAUGHT BY RENDERING LIBRARY` | Layout/paint failure — constraint issues                 |
| `EXCEPTION CAUGHT BY GESTURE`           | Touch handler threw                                       |
| `Unhandled Exception`                   | Uncaught Dart exception — missing try/catch or async gap |
| `NoSuchMethodError`                     | Called method on wrong type or null                       |
| `RangeError`                            | Index out of bounds                                       |
| `StateError`                            | Bad state (e.g., accessing disposed controller)           |

## Emulator Noise — Safe to Ignore

| Pattern                                                                        | Why It's Harmless                         |
| ------------------------------------------------------------------------------ | ----------------------------------------- |
| `W/OpenGLRenderer: Failed to choose config with EGL_SWAP_BEHAVIOR_PRESERVED` | Emulator GPU fallback — no visual impact |
| `W/OpenGLRenderer: Failed to initialize 101010-2 format`                     | HDR format not supported on emulator      |
| `E/OpenGLRenderer: Unable to match the desired swap behavior`                | Despite `E/` level, this is cosmetic    |
| `I/Gralloc4: mapper 4.x is not supported`                                    | Emulator graphics abstraction             |
| `I/Choreographer: Skipped N frames` (N < 50)                                 | Normal during app startup on emulator     |
| `D/FlutterJNI: Beginning load of flutter`                                    | Engine boot sequence                      |

## Informational — Note but Don't Act

| Pattern                                  | Meaning                                    |
| ---------------------------------------- | ------------------------------------------ |
| `I/flutter`                            | App `print()` / `debugPrint()` output  |
| `D/flutter`                            | Framework debug messages                   |
| `Using the Impeller rendering backend` | Normal — Impeller is the default renderer |
| `Syncing files to device`              | Hot sync completing                        |
| `Flutter run key commands`             | App is running and ready                   |
