CanvasLink 0.3.0-alpha.1 is an experimental Android companion for the CanvasTTY integration in draft PR #166.

- Android 8+, phone and tablet layouts, direct terminal input and touch controls.
- LAN discovery and one-time pairing; no separate desktop host app.
- Persistent distribution signing key for subsequent alpha updates.
- APK checksum, public signing certificate fingerprint and CI provenance in `release.json`.
- Earlier debug APKs may have incompatible signatures. The installation prompt preserves existing data and stops on update conflicts.

Requires a desktop built from [PR #166](https://github.com/howdeploy/CanvasTTY/pull/166). It is not included in the official stable desktop release yet.

The APK payload was taken from CI for source commit `eba7baf1f3db716b6600a605f1fda07c39e9119f`, then re-signed without changing payload entries outside `META-INF`. CI success is distinct from physical device acceptance. Windows/Linux device control and this exact signed APK remain unaccepted on hardware.

Read [installation instructions](https://github.com/teo-nex/CanvasLink#installation) or [инструкцию на русском](https://github.com/teo-nex/CanvasLink/blob/main/README.ru.md#установка).
