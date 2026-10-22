# Autotyper 0.1.0 — Windows

```
Autotyper_0.1.0_x64-setup.exe   NSIS installer (2.24 MB)
Autotyper_0.1.0_x64_en-US.msi   MSI installer  (3.39 MB)
SHA256SUMS.txt
```

- Built 2026-10-22 from commit `6ae3a20` (tag `v0.1.0`) with
  `npm run tauri build` on Windows 10/11 x64 (Tauri 2.12, WebView2).
- Replaces the 2026-10-20 build: this one includes the restored
  `typing_preflight` command and the previously missing ACL grants
  (`allow-update-status`, `allow-update-apply`, `allow-open-external`).
- Verified: `target/release/autotyper.exe` contains `allow-settings-load`,
  `allow-typing-preflight`, `allow-update-status`, `allow-update-apply`,
  `allow-open-external`.
- Built with `CARGO_TARGET_DIR` on local disk — the in-repo `target/` was
  corrupted by Nextcloud sync conflicts (see root `AGENTS.md` build gotchas).

Verify:

```powershell
Get-FileHash .\Autotyper_0.1.0_x64-setup.exe -Algorithm SHA256   # compare to SHA256SUMS.txt
```

Install: run the installer (per-user install, no admin prompt), then launch
**Autotyper**. No extra permissions are needed on Windows; F6 starts/pauses and
F7 stops from any application.
