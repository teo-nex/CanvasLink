# Verification receipt · 2026-10-26

## Published artifact

- Release: [v0.3.0-alpha.1](https://github.com/teo-nex/CanvasLink/releases/tag/v0.3.0-alpha.1), marked prerelease.
- APK: `CanvasLink-0.3.0-alpha.1.apk`, 173,354 bytes.
- SHA-256: `0534857896b2e22d7e832a8aaa6146b3fc6acb19f3df857cc9d3e8c1caf5a760`.
- Certificate SHA-256: `0235b1aee591e4f0e24e59484927ead112889521a1b92e40959076d03635b3cb`.
- Downloaded anonymously from the public release URL; hash and `apksigner verify` passed.
- All nine bundled Android asset files match current application source.
- APK payload outside `META-INF` matches the original CI APK byte for byte.
- DEX excludes acceptance instrumentation. Application ID is `io.nexcore.canvaslink`,
  versionCode 3, minimum Android API 26.
- Downloaded release manifest, checksums and both prompt attachments match the repository files.

The APK payload source is `eba7baf1f3db716b6600a605f1fda07c39e9119f`, from
[CI run 40235936427](https://github.com/howdeploy/CanvasTTY/actions/runs/40235936427).
The distribution signature was applied locally after checking that input artifact.
Private signing material is outside both repositories.

## Desktop source and onboarding

Current source: [`f643b31c476e490904437c95c13f0db33ad7c310`](https://github.com/teo-nex/CanvasTTY/commit/f643b31c476e490904437c95c13f0db33ad7c310).
This adds installation guidance to Settings; the Android payload is unchanged.

All eight CI jobs passed for that commit:

| Evidence | Result |
| --- | --- |
| [Desktop CI](https://github.com/howdeploy/CanvasTTY/actions/runs/40243320707) | Five successful jobs: Linux verification, Windows verification, macOS CLI resolution and two mascot pipeline jobs |
| [CanvasLink CI](https://github.com/howdeploy/CanvasTTY/actions/runs/40243320838) | Android APK build and 103 integration tests/typecheck passed |
| [macOS native/package CI](https://github.com/howdeploy/CanvasTTY/actions/runs/40243320634) | Native resource cycles, separately packaged app and bundle signature passed |

Linux general suite: **2,240 passed, 11 skipped, zero failures** (2,251 total).
Windows general suite: **2,116 passed, 135 skipped, zero failures** (2,251 total).
Windows produced NSIS/portable installers. Linux built installers and passed AppImage,
hidden-terminal, Chromium browser and MCP helper smokes. Even G2's 47 tests passed.

Local checks after the settings change: 103 integration tests, three handler tests,
TypeScript, production build and source/built-output secret audit passed. The
handler tests use the existing React stand-in and cover both prompt languages,
absence of pairing/device data in copied text, no host mutation, guide links and
clipboard failure. They do not prove a real OS clipboard or physical device install.

## What these checks do not prove

- Physical Android control on Windows or Linux remains unaccepted.
- The previous macOS/Android prototype was accepted by its user. This exact signed
  APK and the newly packaged source port have not received that acceptance.
- IME, accessibility, rotation, GPU capture and firewall/discovery behavior still
  require physical device testing. No 30 FPS guarantee is made.
- Existing tablet and desktop installations were preserved. The installer prompt
  stops on signature conflicts instead of deleting app data.
- Source PR remains a draft and has not been merged into official CanvasTTY.

See the [source port's fuller verification record](https://github.com/teo-nex/CanvasTTY/blob/feat/canvaslink-android-lan/docs/canvaslink-verification.md)
for earlier local signing/smoke limits, dependency advisories and prototype provenance.
