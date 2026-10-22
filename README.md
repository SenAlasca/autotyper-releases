# Autotyper V4 — releases

Built installers for **Autotyper V4**, one directory per app version, per
platform. This repo only holds binaries + checksums; the source lives in
`autotyper-web`, `autotyper-desktop` and `autotyper-api`.

```
windows/
└── 0.1.0/
    ├── Autotyper_0.1.0_x64-setup.exe     NSIS installer
    ├── Autotyper_0.1.0_x64_en-US.msi     MSI installer
    ├── SHA256SUMS.txt
    └── README.md                         install + verification notes
macos/
└── 0.1.0/
    ├── Autotyper_0.1.0_universal.dmg     Apple Silicon + Intel, macOS 10.15+
    ├── SHA256SUMS.txt
    └── README.md
```

## Current version: 0.1.0 (2026-10-22)

| Platform | File | SHA-256 |
|---|---|---|
| Windows | `Autotyper_0.1.0_x64-setup.exe` | `42d84bcd300d69ea7f7edc4e1810d444159866d16778aff32dddef50ee035199` |
| Windows | `Autotyper_0.1.0_x64_en-US.msi` | `4570ea7134a135d8df69499a4930bb3d9e7df249d016cf88cee6569020ab133d` |
| macOS | `Autotyper_0.1.0_universal.dmg` | `f76b6b4b10a01907c6071b3ad6dbb9603d2ef384c395d128a0b00de6ce31ad6f` |

The same three files are attached to the `v0.1.0` release in
`autotyper-desktop`.

Verify a download:

```powershell
Get-FileHash .\Autotyper_0.1.0_x64-setup.exe -Algorithm SHA256   # Windows
```

```bash
shasum -a 256 -c SHA256SUMS.txt                                  # macOS
```

## macOS first run

The DMG is ad-hoc signed, **not notarized**:

1. Right-click the app → **Open**, or
   `xattr -dr com.apple.quarantine /Applications/Autotyper.app`.
2. **System Settings › Privacy & Security › Accessibility** → enable
   Autotyper, then restart it. Without this, key injection silently does
   nothing (the app's pre-flight blocks Start with an error instead).
3. F6/F7 are media keys unless *Use F1, F2, etc. keys as standard function
   keys* is enabled — otherwise press fn+F6 / fn+F7.

## Adding a version

1. Windows: `npm run tauri build` in `autotyper-desktop` →
   `src-tauri/target/release/bundle/{nsis,msi}/`.
2. macOS: run the `macOS` workflow in `autotyper-desktop` (or
   `npm run tauri build -- --target universal-apple-darwin` on a Mac) →
   download the `autotyper-macos-universal` artifact.
3. Create `windows/<version>/` and/or `macos/<version>/`, drop in the files
   with clean names (no Nextcloud `(conflicted copy …)` suffixes), and add
   `SHA256SUMS.txt`:

   ```powershell
   Get-ChildItem -File | Where-Object { $_.Extension -in ".exe", ".msi", ".dmg" } |
     ForEach-Object { "$((Get-FileHash $_.Name -Algorithm SHA256).Hash.ToLower())  $($_.Name)" } |
     Set-Content SHA256SUMS.txt -Encoding ascii
   ```

4. Commit and push, and attach the same binaries to the matching release in
   `autotyper-desktop`.
