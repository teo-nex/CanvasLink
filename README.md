# CanvasLink for Android

Control your CanvasTTY window from an Android phone or tablet on the same local network.

**Experimental alpha · Android 8+ · macOS prototype accepted by its user.**
Windows and Linux CI builds pass; physical Android control on those hosts is still unverified.

This is a community distribution repository for APKs and installation instructions.
Application source lives in [CanvasTTY](https://github.com/teo-nex/CanvasTTY/tree/feat/canvaslink-android-lan/integrations/canvaslink)
via [draft PR #166](https://github.com/howdeploy/CanvasTTY/pull/166), maintained on the
[contributor branch](https://github.com/teo-nex/CanvasTTY/tree/feat/canvaslink-android-lan/integrations/canvaslink).
The integration has **not been merged into the official stable app**.

[Инструкция на русском](README.ru.md) · [Download alpha APK](https://github.com/teo-nex/CanvasLink/releases/tag/v0.3.0-alpha.1)

[Verification receipt: artifact checks, all eight CI jobs and remaining limits](VERIFICATION.md).

## Installation

You need Android 8 or later, a USB data cable for agent-assisted installation,
and a desktop **built from PR #166** with **Settings → CanvasLink**.
If that section is absent, installing the Android app alone will not add desktop support.
There is no separate desktop CanvasLink application.

1. On Android, enable Developer options and **USB debugging**, then connect the data cable.
2. Unlock Android and approve the computer's RSA authorization dialog. This requires the device owner.
3. Give your local coding agent [this installation prompt](AGENT-PROMPT.en.txt).
   The new desktop settings page can also copy this prompt for you.
4. The agent downloads the pinned APK, verifies SHA-256, selects one authorized
   device and runs `adb -s SERIAL install -r PATH_TO_APK`.
5. Open CanvasLink on Android. Put both devices on the same private Wi-Fi/LAN.
   On the desktop, enable **Settings → CanvasLink → Enable access**.
   Select the discovered computer on Android and enter its one-time six-digit code.

USB is only required for installation. No manual IP entry is normally needed.
Tap a terminal to open the keyboard; Enter executes the input. The app controls
the **whole current CanvasTTY window**, including its Settings and visible terminals.
Desktop access starts off at every launch and can be disabled or revoked in Settings.
Even G2 pairing remains separate.

### Manual installation

Download [CanvasLink 0.3.0-alpha.1](https://github.com/teo-nex/CanvasLink/releases/download/v0.3.0-alpha.1/CanvasLink-0.3.0-alpha.1.apk)
and compare its SHA-256 with [SHA256SUMS](SHA256SUMS) before installation.
You may open the APK on Android and approve installation from your chosen browser/file manager,
or use ADB from [Google Platform-Tools](https://developer.android.com/tools/releases/platform-tools).
Do not enable installation permissions for unrelated apps.

```sh
adb devices -l
adb -s SERIAL install -r CanvasLink-0.3.0-alpha.1.apk
adb -s SERIAL shell am start -n io.nexcore.canvaslink/.MainActivity
```

Use the serial of the intended authorized device. `unauthorized` requires approval
on Android; `offline` requires fixing the connection before retrying.

### Existing development installs

This alpha uses a persistent distribution signing key. Earlier local/CI development
APKs used different keys. Android may reject the update with
`INSTALL_FAILED_UPDATE_INCOMPATIBLE`. **Keep the existing app and its data**;
the agent must stop rather than uninstall, clear data or force a downgrade.
Plan a migration with the device owner. Future releases using this distribution
key and an increased versionCode can update this alpha normally.

## Release provenance

- APK application ID: `io.nexcore.canvaslink`; versionCode: `3`.
- [Release manifest](release.json) pins the download URL, checksum, signing certificate,
  original CI input hash and exact source commit.
- APK payload comes from [CanvasTTY CI run 40235936427](https://github.com/howdeploy/CanvasTTY/actions/runs/40235936427),
  source [`eba7baf`](https://github.com/teo-nex/CanvasTTY/commit/eba7baf1f3db716b6600a605f1fda07c39e9119f).
  It was re-signed locally; all ZIP entries outside `META-INF` were compared byte for byte.
- Private signing material is kept outside this repository and is never included in releases.
- Normal APKs exclude device-acceptance instrumentation.

## Current limits

This is a preview, not an official CanvasTTY release. The previous prototype had
physical macOS/Android acceptance. That does not automatically accept this newly
signed APK and desktop source port. Real device tests of Windows/Linux, IME,
rotation, reconnects and packaged capture still need to be completed.

Eight checks on the original PR commit passed, including Android build and
desktop CI on macOS, Windows and Linux. CI does not prove touch, GPU capture,
network discovery or firewall behavior on every device. Capture fallback may be
around 3–6 FPS; smooth 30 FPS is not promised.

Use a trusted private network. Client isolation can block discovery; a manual
private IPv4 address is available in the Android connection screen. CanvasLink
uses TCP 3499 and mDNS, with no cloud relay. Do not forward this port to the Internet.

See the [full integration guide](https://github.com/teo-nex/CanvasTTY/blob/feat/canvaslink-android-lan/docs/canvaslink.md)
and [verification boundaries](https://github.com/teo-nex/CanvasTTY/blob/feat/canvaslink-android-lan/docs/canvaslink-verification.md).

MIT; bundled Onest font uses SIL OFL 1.1. See [LICENSE](LICENSE),
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and [FONT-LICENSE.txt](FONT-LICENSE.txt).
