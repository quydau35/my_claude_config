# Performance Profiling

## Quick Check

Look at current logs for performance signals:

| Signal | Severity | Meaning |
|---|---|---|
| `Skipped N frames` (N < 50) | Low | Normal on emulator startup |
| `Skipped N frames` (N > 100) | Medium | Main thread blocked |
| `Skipped N frames` (N > 300) | High | Serious jank — investigate |
| Memory warnings | High | Possible leak |
| Excessive widget rebuilds | Medium | Missing `const`, bad state management |

## Profile Mode

For accurate performance data, use profile mode (not debug):

```bash
flutter run --profile -d <device_id> 2>&1
```

Profile mode disables debug assertions but keeps enough instrumentation for timing analysis. Debug mode is too slow for meaningful perf data.

## What to Look For

1. **Frame timing**: Are frames rendering in < 16ms (60fps target)?
2. **Jank spikes**: Sudden frame drops during specific interactions
3. **Memory growth**: Steadily increasing memory = possible leak
4. **Excessive rebuilds**: Widgets rebuilding unnecessarily

## Common Fixes

- **Jank on list scroll**: Use `ListView.builder` instead of `ListView(children:)`
- **Unnecessary rebuilds**: Add `const` constructors, use `Selector` or `select` with Riverpod
- **Heavy computation on main thread**: Move to `compute()` or isolate
- **Large images**: Use `cacheWidth`/`cacheHeight` on `Image` widget
- **Startup jank on emulator**: Usually normal — test on physical device for real numbers
