# Focus: Galaxy Watch 7 (phone-only build prototype)

**Status: source project, NOT yet compiled or device-tested.** The preview is a design illustration, not a screenshot of the rendered watch face. The face XML still uses a basic layout; true liquid-glass rendering and full Focus design are not implemented. A working calendar complication is also not guaranteed until the watch calendar data is tested.

## Build on your Samsung S26 Ultra with GitHub Actions

1. Create a **private** GitHub repository called `focus-watch7` in your phone browser.
2. Upload **the contents of the `MeetingFace` folder**, preserving folders, to the repository root. GitHub's mobile website may be awkward for bulk folders; a Git client app or desktop browser mode can help. Do not upload the ZIP as a single file expecting Actions to unpack it.
3. Open the repository's **Actions** tab and select **Build Focus for Galaxy Watch 7** > **Run workflow**. If Actions runs on push automatically, use that run.
4. If the build succeeds, download the artifact `Focus-Watch7-debug-APKs`. It contains **two APKs**, one from `face` and one from `provider`.
5. On your watch, enable **Developer options** and **Wireless debugging**. Pair the watch with a trusted phone-based ADB client supporting Wear OS pairing code, then install the **provider APK first**, followed by the **face APK**. These are development/debug builds, not Play Store releases.
6. On the watch, open **Meeting Calendar**, grant Calendar access. Select **Meeting Face** as your face, edit the large complication and select **Next meeting and room**.
7. Check that the watch has Google Calendar events accessible through Android CalendarContract. If the card shows **No upcoming meetings** despite scheduled events, watch-local calendar sync is probably unavailable; a separate phone-to-watch sync component would be needed.

## Important limitations

- GitHub Actions is a cloud compiler; it **does not automatically install** APKs onto the watch.
- The project has not been compiled here because an Android SDK/Gradle toolchain was unavailable. The first GitHub Actions run may expose errors; the workflow logs will show them.
- Watch Face Format can render complication text, but long event titles or locations may truncate. Meeting room comes from `CalendarContract.Instances.EVENT_LOCATION`.
- Watch face uses an editable LONG_TEXT center complication and smaller SHORT_TEXT slots. Assign the calendar source manually.
- No Google OAuth credentials are required **if** the watch's calendar provider exposes events. Otherwise, direct cloud integration is future work.
- Do not publish this debug prototype publicly until tested and reviewed.

Reference docs:
https://developer.android.com/codelabs/watch-face-format
https://developer.android.com/training/wearables/complications/exposing-data
