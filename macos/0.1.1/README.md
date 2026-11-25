# Autotyper 0.1.1 — macOS

```
Autotyper_0.1.1_universal.dmg
SHA256SUMS.txt
```

- Universal binary (Apple Silicon + Intel), macOS 10.15 (Catalina) minimum.
- Ad-hoc signed, **not notarized**.
- Built by the `macOS` workflow in `SenAlasca/autotyper-desktop` on
  `macos-latest`: run
  [#45590439276](https://github.com/SenAlasca/autotyper-desktop/actions/runs/45590439276)
  (2026-11-25, 3m42s, success), from commit `b2d524e` on `main` (merge of
  *Fix macOS punctuation injection*), with
  `npm run tauri build -- --target universal-apple-darwin`.
- The same DMG is the `autotyper-macos-universal` artifact of that run. It is
  not attached to a GitHub release in `autotyper-desktop` yet.
- Version metadata inside the bundle still reports **0.1.0** — `package.json`
  and `src-tauri/tauri.conf.json` were not bumped for this build. The release
  folder and DMG filename are 0.1.1.

Verify after copying to a Mac:

```bash
shasum -a 256 -c SHA256SUMS.txt
```

## Install

1. Open the DMG, drag **Autotyper** to *Applications*.
2. First launch: right-click → **Open** (or
   `xattr -dr com.apple.quarantine /Applications/Autotyper.app`) — Gatekeeper
   blocks unnotarized apps on a plain double-click.
3. Grant **System Settings › Privacy & Security › Accessibility** to Autotyper.
   The app prompts once; the UI's pre-flight blocks **Start** with a readable
   error until the switch is on. After enabling it, **restart the app**.
   Unsigned builds are keyed to their code signature, so **re-grant after every
   rebuild**.
4. F6/F7 are media keys on Mac keyboards unless *Use F1, F2, etc. keys as
   standard function keys* is enabled — otherwise press fn+F6 / fn+F7.

## What changed

- Fix macOS punctuation injection (merge `b2d524e`).
- Rebuilt on `macos-latest` from current `main`.
