# Auto-Diagnose & Fix Cycle

The full RED→GREEN loop applied to runtime bugs.

## The Cycle

```
🔴 RED:      Launch app → crash detected
🔍 DIAGNOSE: Read error + stack trace → identify root cause
🔧 FIX:      Edit source code
✅ VERIFY:   Run tests → all pass
🟢 GREEN:    Relaunch → crash gone
🔄 REPEAT:   New error? → back to RED
```

## Step by Step

### 1. RED — Observe the crash

Launch the app ([launch.md](launch.md)). Read logs ([logs.md](logs.md)). Extract the error.

### 2. DIAGNOSE — Find root cause

From the stack trace, identify:
- **What** threw (the exception type and message)
- **Where** it threw (the source file and line)
- **Why** it threw (the logical cause — missing init, wrong type, null, etc.)

### 3. FIX — Edit the code

Make the minimal change to fix the root cause. Don't refactor — just fix.

### 4. VERIFY — Run tests

```bash
flutter test
```

If tests break, the fix introduced a regression. Revise the fix.

### 5. GREEN — Relaunch

Stop the old process, relaunch ([lifecycle.md](lifecycle.md)). Confirm the error is gone.

### 6. REPEAT

If a new error appears, start a new cycle. Report iterations clearly:

```
🔴 Cycle 1: HiveError — Hive.init(null) fails on Android
   Fix: Changed to Hive.initFlutter() with await
🟢 Cycle 1: Resolved

🔴 Cycle 2: UnimplementedError — Provider not wired to GetIt
   Fix: Connected todoControllerProvider to getIt<TodoController>()
🟢 Cycle 2: Resolved — app rendering
```

## When to Stop

- App launches without errors → done
- App renders the expected UI → done
- User says to stop → done
- After 5 cycles with no progress → escalate to user, something deeper is wrong
