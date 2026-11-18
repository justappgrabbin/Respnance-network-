# Archive parts

Upload all four original binary archive parts into this directory in **one commit**, using GitHub's **Add file → Upload files**. These are consecutive binary chunks, **not individual ZIP archives**.

Each file is 18,649,551 bytes. The build workflow reassembles them, validates the four part checksums plus original archive checksum from `../archive-manifest.json`, extracts `organism/frontend/`, builds the existing React/Vite app, and produces a Capacitor Android debug APK as a workflow artifact.

Do not rename the parts or try to unzip them independently.

**Publication notice:** This original archive includes saved databases, learning assets and project source. This repository is public; review what you are publishing before uploading the four parts.
