# Resonance Network — four-part verified archive and Android APK build

This repository preserves the original `Resonance-Network-Social-Organism-Merged.zip` **byte-for-byte** as four consecutive binary chunks.

The archive was retrieved from the owner's Google Drive and verified against its recorded original SHA-256.

**Original archive size:** 74,598,204 bytes  
**Original SHA-256:** `2b295c6e76f84ac0a5bdadf3fef71c50380e7bd6ce1e23fd49d8efdc3cfa2a56`

## Upload the four parts

Open [archive-parts/](archive-parts), choose **Add file → Upload files**, and select all four files **in one commit**:

- `Resonance-Network-Social-Organism-Merged.zip.part01-of-04`
- `Resonance-Network-Social-Organism-Merged.zip.part02-of-04`
- `Resonance-Network-Social-Organism-Merged.zip.part03-of-04`
- `Resonance-Network-Social-Organism-Merged.zip.part04-of-04`

All four parts are 18,649,551 bytes. They are binary chunks, not individually extractable ZIPs. The [manifest](archive-manifest.json) contains each part's SHA-256 checksum.

**Public-repository notice:** The archive includes source code, SQLite databases, and learning/reference assets. Review what you are publishing before uploading: the repository is public.

## Automatic Android APK build

After the four parts arrive, [GitHub Actions](https://github.com/justappgrabbin/Respnance-network-/actions/workflows/build-resonance-apk.yml) automatically:

1. Concatenates the four binary parts in order.
2. Verifies every part checksum plus the original whole-ZIP checksum and ZIP integrity.
3. Extracts the unmodified archive and locates `organism/frontend`.
4. Installs its locked npm dependencies and builds the existing React/Vite frontend.
5. Uses the **existing Capacitor 8 configuration** to generate the Android native project.
6. Runs Gradle to build an **installable debug APK**.
7. Uploads `resonance-network-android-debug-apk` in the completed workflow run's **Artifacts** section.

The workflow can also be started with **Actions → Reassemble Resonance Network and Build Android APK → Run workflow**.

## API connectivity

The original frontend calls a Python/FastAPI backend. An Android APK does **not** itself host that Python backend. To enable network-backed features, deploy the backend separately and set the GitHub Actions repository variable `RESONANCE_API_BASE_URL` to its externally reachable HTTPS API base URL (typically ending in `/api`) **before building**. Alternatively, the original Welcome screen provides a server-address override.

A successful APK build establishes installability, not end-to-end backend availability.

This workflow builds a **debug APK** for direct installation/testing; it does not create a Play Store signed production release.

## Reassemble locally

macOS/Linux:

```bash
cat archive-parts/*.part0?-of-04 > Resonance-Network-Social-Organism-Merged.zip
sha256sum Resonance-Network-Social-Organism-Merged.zip
```

Windows PowerShell:

```powershell
$files = 1..4 | ForEach-Object { "archive-parts/Resonance-Network-Social-Organism-Merged.zip.part$($_.ToString('00'))-of-04" }
$out = [System.IO.File]::Create("Resonance-Network-Social-Organism-Merged.zip")
try { foreach ($f in $files) { $input = [System.IO.File]::OpenRead($f); try { $input.CopyTo($out) } finally { $input.Dispose() } } } finally { $out.Dispose() }
Get-FileHash Resonance-Network-Social-Organism-Merged.zip -Algorithm SHA256
```

Do not extract the individual parts; reassemble first.
