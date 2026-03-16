# Collect & Analyze Logs

## Reading Output

Read the background task output using `TaskOutput` (non-blocking) or `Read` on the output file.

## Categorize

Parse every line into one of these:

- **🔴 ERRORS**: `E/flutter`, `EXCEPTION CAUGHT`, `Unhandled Exception`
- **⚠️ WARNINGS**: `W/`, `WARNING` (skip emulator noise — see [log-patterns.md](log-patterns.md))
- **📋 INFO**: `I/flutter`, `D/flutter`
- **🐛 DEBUG PRINTS**: `print()` / `debugPrint()` output from app code

## For Each Error

Provide:

1. The error message (one line)
2. The stack trace (trimmed to app frames — skip framework internals)
3. The source file and line number
4. A suggested fix with rationale

## Example Output

```
🔴 ERROR: HiveError: You need to initialize Hive or provide a path
   at lib/di.dart:74 — initHive()
   Cause: Hive.init(null) doesn't resolve a path on Android
   Fix: Use Hive.initFlutter() from hive_flutter package

⚠️ 2 warnings (emulator GPU noise — ignored)
📋 3 info lines (Impeller backend, sync complete)
```
