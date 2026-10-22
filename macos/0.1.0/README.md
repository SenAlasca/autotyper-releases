# Autotyper 0.1.0 — macOS

```
Autotyper_0.1.0_universal.dmg
SHA256SUMS.txt
```

- Universal binary (Apple Silicon + Intel), macOS 10.15 (Catalina) minimum.
- Ad-hoc signed, **not notarized**.
- Built by the `macOS` workflow in `SenAlasca/autotyper-desktop` on
  `macos-latest`: run
  [#39768949012](https://github.com/SenAlasca/autotyper-desktop/actions/runs/39768949012)
  (2026-10-22, 3m34s, success), from commit `6ae3a20` / tag `v0.1.0`, with
  `npm run tauri build -- --target universal-apple-darwin`.
- Also attached to the GitHub release `v0.1.0`.

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

## Not verified yet on real hardware

The build is compile-checked and bundled, but the macOS runtime behaviour is
untested: the Accessibility prompt/guard path, `NSAppSleepDisabled`, WebKit
timer throttling while the window is occluded, HUD transparency, and key
injection into native vs. Electron targets. See `apps/desktop/AGENTS.md`
§ macOS support.
