# mapartbridge-packs

Public resource-pack origin for the **MapArtBridge RGB** Minecraft plugin.

## What this is

Each release carries the Java resource packs that make map art show **24-bit colour** without any client mod.
One ZIP per Minecraft version; the file name *is* the content hash:

```
<mcver>-<sha1>.zip      e.g. 26.3-2f2548f571f8b7ceb293b945961bb582bd1c831a.zip
```

The plugin points clients at

```
https://github.com/OWNER/mapartbridge-packs/releases/latest/download/{file}
```

so a new release needs **no config change**: the plugin rebuilds only when a new image arrives, the file name
changes with its SHA-1, and clients fetch exactly the pack their server announced.

## Integrity

- asset name must equal `<mcver>-<sha-1 of the file>`; the publisher refuses anything else;
- every asset is downloaded back and re-hashed after upload;
- each release ships `SHA256SUMS` and `manifest.json` (`mc`, `packFormat`, `file`, `sha1`, `sha256`, `bytes`);
- the Minecraft client itself verifies the SHA-1 the server sends, so a corrupted file is rejected client-side.

## Privacy warning

The ZIPs contain player-submitted images as 128x128 textures. **This repository is public**, so those images
are publicly downloadable. Do not publish packs for private art without the owner's consent.

## Publishing

Done by the operator's tool `github_publish.py` (reads pack files from the Minecraft server via SFTP, verifies,
uploads, re-verifies). Manual alternative: `gh release create packs-<stamp> ./*.zip SHA256SUMS manifest.json --latest`.

Do not rename assets, do not overwrite an existing asset name, do not upload pack files > 100 MB.
