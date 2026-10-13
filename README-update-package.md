# VibeCast Crash Notification + APK Build Update

This package contains the update files for the crash notification feature and GitHub Actions APK build workflow.

## Included files

- `vibecast/src/main/kotlin/io/github/tukiza7_debug/vibecast/crash/CrashReporter.kt`
- `.github/workflows/build-apk.yml`
- `CHANGELOG.md`

## Crash notification behavior

When an uncaught crash occurs, the updated `CrashReporter`:
- writes the last crash report to `filesDir/last-crash.txt`
- creates a notification channel if required
- posts a high-priority notification titled `VibeCast crashed`
- opens the app when the notification is tapped
- keeps the existing crash dialog flow intact for user diagnostics

## CI workflow behavior

The workflow automatically:
- checks out the repository
- sets up Java 17
- caches Gradle dependencies
- runs unit tests
- assembles debug + release APKs
- uploads APK artifacts and optional ProGuard mapping file

## Notes

- Release APK signing requires repository secrets:
  - `RELEASE_KEYSTORE_B64`
  - `RELEASE_KEYSTORE_PASSWORD`
  - `RELEASE_KEY_ALIAS`
  - `RELEASE_KEY_PASSWORD`
- If those secrets are not set, debug build can still complete, but signed release may fail.
