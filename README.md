# Resonance Network archive — unchanged, three-part transfer

The original file `Resonance-Network-Social-Organism-Merged.zip` is kept byte-for-byte unchanged. For GitHub transfer it is divided into three consecutive binary parts; these are **not** individually extractable ZIPs.

Download all three files from the `archive-parts/` folder and concatenate in numeric order.

macOS/Linux:
```sh
cat archive-parts/Resonance-Network-Social-Organism-Merged.zip.part0{1,2,3}-of-03 > Resonance-Network-Social-Organism-Merged.zip
shasum -a 256 Resonance-Network-Social-Organism-Merged.zip
```

Windows PowerShell:
```powershell
$files = 1..3 | ForEach-Object { "archive-parts/Resonance-Network-Social-Organism-Merged.zip.part$($_.ToString('00'))-of-03" }
$out = [System.IO.File]::Create("Resonance-Network-Social-Organism-Merged.zip")
try { foreach ($f in $files) { $input = [System.IO.File]::OpenRead($f); try { $input.CopyTo($out) } finally { $input.Dispose() } } } finally { $out.Dispose() }
Get-FileHash Resonance-Network-Social-Organism-Merged.zip -Algorithm SHA256
```

Original archive size: `74598204` bytes.

Original SHA-256:
`2b295c6e76f84ac0a5bdadf3fef71c50380e7bd6ce1e23fd49d8efdc3cfa2a56`

Only the transport representation is divided; archive contents and original archive bytes are not edited.
