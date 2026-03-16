# Stop & Restart

## Stop

Stop the running background task:

```
TaskStop with the saved task ID
```

The `flutter run` process will terminate and the app will close on the device.

## Restart

After code changes, stop and relaunch:

1. Stop the current process (TaskStop)
2. Run tests to verify changes (`flutter test`)
3. Relaunch: `flutter run --debug -d <device_id> 2>&1` (background)
4. Monitor startup as in [launch.md](launch.md)

## Why Not Hot Reload?

Background processes are non-interactive — `stdin` is not a TTY, so pressing `r` for hot reload is not possible. The only way to apply code changes is the full stop → relaunch cycle.

For interactive hot reload, the user should run `flutter run` in their own terminal instead.
