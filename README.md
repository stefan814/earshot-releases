<p align="center">
  <img src="docs/icon.png" width="128" alt="Earshot icon">
</p>

<h1 align="center">Earshot</h1>

<p align="center">
  <b>Every call, transcribed on your own computer, and ready for your AI agent.</b><br>
  Earshot sits in your menu bar (or system tray), notices when a call starts in any app, and writes a clean transcript: you on one side, everyone else on the other. Nothing leaves your machine.
</p>

<p align="center">
  <a href="https://github.com/stefan814/earshot-releases/releases/latest"><img src="https://img.shields.io/github/v/release/stefan814/earshot-releases?label=release" alt="Latest release"></a>
  <img src="https://img.shields.io/badge/macOS-26%2B%20%C2%B7%20Apple%20silicon-black" alt="macOS 26+, Apple silicon">
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-0078D4" alt="Windows 10 and 11">
  <img src="https://img.shields.io/badge/Android-13%2B-3DDC84" alt="Android 13+">
  <img src="https://img.shields.io/badge/MCP-built%20in-6E56CF" alt="MCP server built in">
  <img src="https://img.shields.io/badge/price-free-2EA44F" alt="Free">
</p>

---

- [Why Earshot](#why-earshot)
- [Install](#install)
- [Features](#features)
- [Phone app for in-person meetings](#phone-app-for-in-person-meetings)
- [How it works](#how-it-works)
- [For AI agents (MCP)](#for-ai-agents-mcp)
- [Privacy and your data](#privacy-and-your-data)
- [Settings](#settings)
- [Updates](#updates)
- [Feedback](#feedback)
- [Troubleshooting](#troubleshooting)
- [Credits](#credits)

## Why Earshot

- **It just starts.** No calendar to connect and no bot joining the call. When Zoom, Teams, Meet or any other call app starts using your microphone, Earshot starts transcribing. It also catches calls you join just to listen, with your mic off: Zoom's app, and Meet, Zoom, Teams and other call sites in the browser. When the call ends, it stops.
- **It knows when you're muted.** Earshot reads the mute button in the call app. Whatever you say while muted stays out of the transcript.
- **"Me" and "Them", always.** Your microphone and the call's audio are recorded separately, so every line is attributed correctly. The full edition also tells the other people apart.
- **Built for agents.** A local MCP server lets Claude, Codex, Cursor or any other MCP client read, search and control your calls. Ask "what did we agree on in my 2pm?" and your agent has the transcript.
- **Private by design.** Speech recognition runs on your computer. Audio is never sent anywhere and isn't kept.

## Install

**Mac** (Apple silicon, macOS 26 or later). Open Terminal and paste:

```bash
curl -fsSL https://github.com/stefan814/earshot-releases/releases/latest/download/install.sh | bash
```

**Windows** (10 or 11, x64 or ARM). Open PowerShell and paste:

```powershell
irm https://github.com/stefan814/earshot-releases/releases/latest/download/Install-Earshot.ps1 | iex
```

On Windows the installer adds Microsoft's .NET 10 runtimes if they're missing (Windows asks for permission first), then downloads the speech models (about 54 MB).

Both commands install **Earshot Lite**. For the full edition, which also tells the other people on a call apart:

| | Mac | Windows |
|---|---|---|
| **Lite** (default) | 1 MB · Me / Them | about 8 MB · Me / Them |
| **Full** | 100 MB · Me / Speaker 1, 2, 3… | about 8 MB + a 23 MB model · Me / Speaker 1, 2, 3… |
| Install Full | add `-s -- --full` after `bash` | `& ([scriptblock]::Create((irm <the address above>))) -Full` |

> **Why a command instead of a download?** Earshot isn't signed with a paid Apple or Microsoft certificate. Files a browser downloads get a "downloaded from the internet" mark, and macOS and Windows warn about those. Files the install command fetches don't get that mark, so there's no warning to click through.
>
> Prefer a regular download? Get the `.dmg` (Mac) or `Earshot-Setup-….exe` (Windows) from the [latest release](https://github.com/stefan814/earshot-releases/releases/latest). On a Mac, the first time you open it, go to **System Settings → Privacy & Security → Open Anyway**. On Windows, click **More info → Run anyway**.

**Android phone** (Android 13 or later), for in-person meetings: on the phone, download `Earshot-…-android.apk` from the [latest release](https://github.com/stefan814/earshot-releases/releases/latest) and open it. Android asks once to allow installs from your browser. See [Phone app](#phone-app-for-in-person-meetings).

The first time it runs, Earshot asks for:
- **Microphone**, for your side of the call.
- **System audio** (Mac), for everyone else.
- **Accessibility** (Mac, optional), for meeting titles, mute buttons and participant names.

## Features

| | Feature | |
|---|---|---|
| 🎙️ | **Automatic start and stop** | Zoom, Teams, Google Meet, Slack huddles, FaceTime, Webex, Discord, WhatsApp, Telegram, Skype, RingCentral, and calls in Chrome, Edge, Arc, Brave, Firefox, Safari and other browsers. |
| 🎧 | **Calls you only listen to** (Mac) | Joined without your mic? Zoom's app is caught by its meeting window (with Accessibility on). In the browser, the Chrome extension sees the call on Google Meet, Zoom, Teams, Slack, Webex, Whereby and Jitsi, and on any site you add at the bottom of **Record Calls From** in the menu. Your mic stays off until the call turns it on. |
| 🔇 | **Mute awareness** | Reads the call app's mute button. On web calls, the Chrome extension also checks whether the page is actually sending your audio. Muted speech is left out. |
| 👥 | **Speaker separation** (Full) | NVIDIA's Sortformer model on Mac and a speaker-embedding model on Windows turn "Them" into Speaker 1, 2, 3…, entirely on your computer. Rename speakers from your agent. |
| 🏷️ | **Names and titles** | With Accessibility on (Mac), Earshot takes the meeting topic, the participant list and who's talking from Zoom and Google Meet captions and from Teams' and Slack huddles' speaking highlight. On Windows: Google Meet (through the Chrome extension) and Slack huddles. The transcript text is still Earshot's own. A call with no title is named after the app and time ("Slack call — Nov 16, 3:04 PM"); your agent can rename it. |
| 💬 | **Chat and shared links** | Zoom and Google Meet chat messages, and links shared in the call, are saved with the meeting. |
| 🎚️ | **Choose which calls** | **Record Calls From** in the menu has a switch for each call app you have installed and each web service, so you can leave out, say, FaceTime or Discord. A service's switch covers its calls in the app and in the browser; a browser's own switch covers calls on other sites. For a single call, **Pause Recording** in the menu stops the transcript until you resume, and **Pause Earshot** stops it watching for calls at all. |
| 📱 | **In-person meetings** | The phone app transcribes meetings in the room and sends them to Earshot on your Mac or Windows PC, where they join your other meetings and your agent can read them. |
| 🌐 | **Languages** | English plus Chinese (Mandarin), Hindi, Spanish, Arabic, French, Bengali, Portuguese, Russian, Indonesian and German. On first run Earshot asks which ones your calls are in, shows what each costs to download, and downloads nothing until you continue; switch the language for the next call from the menu (**Transcribe In**). Mac uses Apple's on-device speech for all of them. Windows and the phones download Moonshine (Chinese, Spanish, Arabic) or NVIDIA Parakeet v3 (French, Portuguese, Russian, German); Hindi, Bengali and Indonesian use the phone's own recognizer and are coming later on Windows. Change them any time in Settings ▸ Languages. |
| 🤖 | **MCP server** | 16+ tools for listing, reading, searching and controlling meetings. Works with any MCP client. |
| ♻️ | **Picks up where it left off** | If Earshot quits, crashes or the computer sleeps mid-call, the same meeting carries on instead of splitting into fragments. |
| 🩺 | **Health checks** | Earshot watches for anything that would quietly stop it recording (a permission switched off, a full disk, a missing model) and shows a fix in its menu. |
| ⬆️ | **One-click updates** | It offers new versions itself and installs them when you click. Never during a call. |

<p align="center">
  <img src="docs/menu.png" width="420" alt="The Earshot menu, with Record Calls From open">
  &nbsp;&nbsp;&nbsp;
  <img src="docs/about.png" width="330" alt="About Earshot">
</p>

### Who's who

- **You** are "Me": your microphone is recorded on its own, so this needs no voice training. Anyone sitting at your computer with you shares your mic, so they're "Me" too.
- **Everyone on the other end** gets their real name when the call app shows it (captions, the participant list, who's highlighted as speaking). When it can't, the Full edition tells voices apart by sound: Speaker 1, 2, 3…. That includes several people sharing one mic in a meeting room, since the call app sees them as one participant. Lite calls anyone it can't name "Them".
- **On the phone**, everyone in the room comes through one mic, so it goes by voice alone: teach it your voice and you're "Me", and everyone else is Speaker 1, 2, 3….

You can rename any speaker from your agent.

## Phone app for in-person meetings

Earshot on your computer hears calls. For meetings in a room, put your phone on the table and tap Record.

<p align="center">
  <img src="docs/phone.png" width="760" alt="The Earshot phone app: ready to record, transcribing, settings, and dark mode">
</p>

- **Transcribed on the phone, your choice of model.** Before your first recording, the app asks how to turn speech into text: NVIDIA Parakeet, a 136 MB download kept either in the phone's shared models (so our other apps can use the same copy, via [Garden](https://github.com/stefan814/garden)) or for Earshot only, or the speech recognition already built into the phone (Apple's on iPhone; Android's own, if the phone has its language installed). The app recommends Parakeet in the shared models: in our tests it got about half as many words wrong as the built-in recognizers when people talk across a room (5–9% against 10–12%). The choice is yours, and you can change it later in Settings ▸ Speech model. Everything runs on the phone, and audio is never stored.
- **Sent to your computer over Bluetooth.** Open the Earshot menu (the tray menu on Windows) ▸ **Settings ▸ Pair a Phone (In-Person Meetings)…**. Scan the code it shows with the phone (in the app's Settings, tap **Pair with a computer**). After that, finished meetings go to the computer by themselves when the two are near each other, or when you tap Send. The phone deletes its copy once the computer confirms it has it. The transfer is encrypted with a key made at pairing. A phone pairs with one computer at a time.
- **Knows your voice.** In Settings, **Teach my voice** has you read a short passage aloud. Your lines are then marked "Me", and other people become Speaker 1, 2, 3…. Only a voiceprint is kept.
- **Record from anywhere.** A one-tap record button for the home screen (Android and iPhone), a Quick Settings tile (Android), and Lock Screen and Control Center buttons (iPhone). The button turns green while recording and yellow while the transcript is saved.
- **Tells you about updates.** About twice a day it checks whether a newer Earshot is out. If so, you get one notification, a mark on the app icon (a dot on Android, a badge on iPhone) and a banner on Earshot's home screen. Tapping the notification opens that banner. **Not now**, or swiping the notification away, clears the mark. On Android, **Update** downloads it, checks it against the release's fingerprint and opens Android's installer (Android asks once to allow installs from Earshot). Turn it off in Settings ▸ Updates.
- **Handy extras.** Meetings can be named from your calendar (read on the phone only), recording keeps going with the screen off, and it stops by itself after a stretch of silence.

<p align="center">
  <img src="docs/widget.png" width="460" alt="The record button: ready (white) and recording (green), on Android and iPhone">
</p>

<p align="center">
  <img src="docs/windows-phone.png" width="420" alt="Pairing a phone on Windows: the Earshot on Your Phone window with its QR code">
</p>

**On Windows**, the PC's Bluetooth adapter has to accept connections from a phone. Most built-in adapters do; some USB dongles don't, and the pairing window says so if yours can't.

**Android:** download the `.apk` from the latest release (see [Install](#install)). It's about 39 MB; if you choose Parakeet, the app downloads it once (136 MB). A newer version installs over the old one and keeps your meetings and pairing.

**iPhone (iOS 26):** there's no App Store version yet. It can be built from Earshot's source with Xcode and installed on your own iPhone with a free Apple account. The source isn't public yet, so for now this is for people who have access to it.

The phone apps only transcribe meetings in the room. Phones don't let other apps capture a Zoom, Meet or phone call's audio, so calls are transcribed by Earshot on your computer instead.

## How it works

```
  call app opens the mic, or a call's ──► Earshot notices (within a second)
  meeting window or web page appears
                                   │
            ┌──────────────────────┴──────────────────────┐
     your microphone                                 the call's audio
            │                                              │
   mute check (call app's button,                  speaker separation
   or the page via the extension)                  (Full edition)
            │                                              │
            └───────────► on-device speech to text ◄───────┘
                     (Apple SpeechAnalyzer on Mac,
                      Moonshine on Windows)
                                   │
              ~/.earshot/meetings/<date_time_app>/
               transcript.md · transcript.jsonl · meeting_info.json
                                   │
                    MCP server on 127.0.0.1:8796 ──► your AI agent
```

A call ends when the call app stops using the microphone and speakers for 25 seconds, or when its meeting window closes. In a browser it ends 25 seconds after the call does (the browser's mic, or the call the extension sees in the tab), even if the browser keeps playing sound. You can also start and stop by hand from the menu or through MCP.

## For AI agents (MCP)

Earshot runs an MCP server at `http://127.0.0.1:8796/mcp` (Streamable HTTP), on this computer only. The menu's **Settings ▸ Copy MCP Server URL** copies the address (the tray menu's, on Windows).

**Claude Code:**

```bash
claude mcp add --transport http --scope user earshot http://127.0.0.1:8796/mcp
```

For any other client, add an HTTP MCP server with that address.

| Tool | What it does |
|---|---|
| `earshot_get_status` | Whether a call is being recorded, which app holds the mic, health problems |
| `earshot_list_meetings` | Recent meetings with titles, apps, times and lengths |
| `earshot_get_transcript` | A meeting's transcript (the current one if none is given) |
| `earshot_search_transcripts` | Search every transcript |
| `earshot_get_meeting_status` | Details of the meeting in progress |
| `earshot_get_chat` · `earshot_get_shared` | Chat messages and links shared in a call |
| `earshot_rename_speaker` | Put a name on "Speaker 2", or list a meeting's speakers |
| `earshot_start_capture` · `earshot_stop_capture` | Start or stop a recording by hand |
| `earshot_pause_capture` · `earshot_resume_capture` | Pause for an off-the-record moment |
| `earshot_start_monitoring` · `earshot_stop_monitoring` | Turn automatic recording on or off |
| `earshot_archive_meeting` · `earshot_delete_meeting` | Tidy up |

Earshot doesn't summarize. That's your agent's job, with whichever model you choose, so Earshot itself never needs an AI service.

## Privacy and your data

- Speech recognition, speaker separation and mute detection all run on your computer.
- **Telling people is up to you.** Recording laws vary, and some places need everyone's consent. Earshot doesn't join the call as a bot, so nobody else can see it's recording.
- Audio is transcribed as it arrives and then discarded. To keep recordings too, set `"saveAudio": true`. They're silent wherever you were muted.
- The MCP server only listens on `127.0.0.1`, so other computers can't reach it. The Chrome extension can only talk to Earshot, and Earshot rejects requests from web pages.
- The phone app talks to your paired computer over Bluetooth, and its waiting meetings are encrypted on the phone. It uses the internet only to download the Parakeet speech model, if you choose it, and to check for a newer version twice a day (you can turn that off). Downloads are checked against a fixed fingerprint and nothing is uploaded.
- The only network requests are the speech-model downloads (Windows install; Parakeet on the phone, if you choose it) and a small check for new versions twice a day (computer and phone), which you can turn off.

Everything is in a folder you own:

```
~/.earshot/
├── config.json                    settings
├── earshot.log
└── meetings/
    └── 2026-11-03_141502_zoom/
        ├── transcript.md          readable transcript
        ├── transcript.jsonl       one line per utterance, with times and speakers
        ├── meeting_info.json      app, title, start/end, participants
        ├── speakers.jsonl         who spoke when
        └── chat.jsonl             chat messages, if any
```

A transcript looks like this:

```
[14:15:02] Me: Can you walk me through how you got to that estimate?
[14:15:07] Speaker 1: Sure, we took the average of the last three months.
[14:15:15] Speaker 2: And adjusted for the holiday dip.
```

## Settings

Edit `~/.earshot/config.json` (Windows: `%USERPROFILE%\.earshot\config.json`) and restart Earshot.

| Setting | Default | |
|---|---|---|
| `checkForUpdates` | `true` | Look for new versions twice a day |
| `locale` | `"en-US"` | Which English Earshot uses, e.g. `"en-GB"` (Mac). Other languages are picked in **Languages…** in the menu. |
| `saveAudio` | `false` | Also keep the audio of each call |
| `detectAnyApp` | `false` | Treat any app that uses the mic as a call, not just known call apps |
| `apps` | built-in list | Which apps count as call apps |
| `minMicSeconds` | `3` | How long an app must hold the mic before a meeting starts |
| `endAfterSilentSeconds` | `25` | How long a call app must be silent before the call counts as over |
| `port` | `8796` | The MCP server's port |

## Updates

When a new version is out, Earshot shows one notification and an **Update to Earshot X…** item in its menu. Click either one and Earshot updates and restarts in a few seconds, keeping your edition, permissions and meetings. If you're on a call, it waits until the call ends. Running the install command again also updates.

The phone app checks too, from version 0.7.5: a banner on its home screen, and on Android one tap to download and install. Phones on an older version need the new `.apk` once, by hand.

## Feedback

Something not working, or an idea? Use **Send Feedback**: on the Mac and Windows it's in Earshot's menu (Settings ▸ Send Feedback…), and on the phone it's in Settings ▸ Feedback. Write what happened and Earshot attaches its logs to an email to earshotproject@gmail.com. You see the email before it's sent. The logs include meeting titles, but never transcripts or audio.

## Troubleshooting

**Nothing is recorded during calls.** Open the Earshot menu: problems are listed at the top with a **Fix…** button. Most often it's a permission that was switched off.

**Everyone else shows up as silence (Mac).** Allow Earshot under System Settings → Privacy & Security → Screen & System Audio Recording.

**No meeting titles or participant names (Mac).** Allow Earshot under Privacy & Security → Accessibility.

**My words were transcribed while I was muted.** Earshot reads the call app's own mute button; a hardware mute switch or muting in system settings isn't visible to it. For web calls, install the Chrome extension from the menu (**Settings ▸ Set Up Chrome Extension…**).

**After updating to 0.6.1, macOS asked for permissions again.** Expected once. Earshot's internal name changed from its old one, so macOS treats it as a new app. You can remove the old SuperCall entries from each list in System Settings → Privacy & Security.

**Other people's words show up as "Me".** On speakers, the call's sound can leak into your microphone. Earshot cancels the echo and drops lines that repeat what the other side said, but headphones avoid it completely.

**Windows blocks it completely.** On PCs with Smart App Control turned on, Windows blocks apps without a paid signature, and there's no "run anyway". It's off on most PCs.

## Credits

Earshot is free to use. It's built on:
- Apple's SpeechAnalyzer.
- [Moonshine](https://github.com/moonshine-ai/moonshine) speech recognition and [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx).
- The [Silero VAD](https://github.com/snakers4/silero-vad) voice detector.
- NVIDIA's Streaming Sortformer model via [FluidAudio](https://github.com/FluidInference/FluidAudio), under the NVIDIA Open Model License.
- NVIDIA NeMo SpeakerNet.
- Phone app: NVIDIA [Parakeet TDT 110M](https://huggingface.co/nvidia/parakeet-tdt_ctc-110m) speech recognition and NVIDIA NeMo TitaNet-small voiceprints (both CC-BY-4.0), run with [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx); [Moonshine](https://github.com/moonshine-ai/moonshine) (Chinese, Spanish, Arabic) and NVIDIA [Parakeet TDT 0.6B v3](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3) (CC-BY-4.0; French, Portuguese, Russian, German) on Windows and the phones; Android's and Apple's built-in speech recognition (SpeechTranscriber on iPhone); the CAM++ voiceprint model ([3D-Speaker](https://github.com/modelscope/3D-Speaker), via FluidAudio) on iPhone.
