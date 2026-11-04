# Earshot

Earshot transcribes your calls (Zoom, Google Meet, Teams, Slack, FaceTime and others) on your own computer. Audio and transcripts stay on your machine. The only network traffic is the speech-model download when you install (Windows) and a small check for new versions, which you can turn off.

## Install

**Mac** needs Apple silicon and macOS 26 or later. Open Terminal and paste:

```
curl -fsSL https://github.com/stefan814/earshot-releases/releases/latest/download/install.sh | bash
```

For Earshot Lite (no speaker separation, a much smaller download), add `-s -- --lite` after `bash`.

**Windows** needs Windows 10 or 11 (x64 or ARM). Open PowerShell and paste:

```
irm https://github.com/stefan814/earshot-releases/releases/latest/download/Install-Earshot.ps1 | iex
```

If Microsoft's .NET 10 runtimes are missing, the installer adds them (Windows asks for permission first), then downloads the speech models (about 54 MB).

Installing this way skips the "unidentified developer" (Mac) and "Windows protected your PC" warnings, because the files never get a downloaded-from-the-internet mark. You can also download the disk image or Setup.exe from the [latest release](https://github.com/stefan814/earshot-releases/releases/latest).
- **Mac:** the first time you open it, go to System Settings → Privacy & Security and click **Open Anyway**.
- **Windows:** click **More info** → **Run anyway**.

## Updates

Earshot checks for new versions twice a day. When one is out, it shows a notification and an "Update to Earshot X…" menu item. Click it and Earshot updates and restarts on its own, never during a call. To stop the checks, set `"checkForUpdates": false` in `~/.earshot/config.json` (Windows: `%USERPROFILE%\.earshot\config.json`).

Each download has a matching `.sha256` checksum file.
