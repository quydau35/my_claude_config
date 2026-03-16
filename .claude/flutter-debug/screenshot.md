# Screenshot Capture

## Capture

Use `adb` to grab a screenshot from the device:

```bash
adb -s <device_id> exec-out screencap -p > /tmp/flutter_debug_screenshot.png
```

For emulators, `<device_id>` is typically `emulator-5554`.

## View

Present the screenshot using the Read tool, which supports image files:

```
Read /tmp/flutter_debug_screenshot.png
```

## UI Diagnosis

When the user describes a visual issue:

1. Capture the screenshot
2. Show it to confirm you see the same thing
3. Cross-reference with widget source code:
   - Identify the widget responsible for the area
   - Check layout constraints, colors, text styles
   - Look for overflow, clipping, or missing content
4. Propose a fix targeting the specific widget

## Multiple Captures

For before/after comparisons, use timestamped filenames:

```bash
adb -s emulator-5554 exec-out screencap -p > /tmp/flutter_debug_before.png
# ... apply fix, relaunch ...
adb -s emulator-5554 exec-out screencap -p > /tmp/flutter_debug_after.png
```
