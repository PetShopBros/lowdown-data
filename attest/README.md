# Lowdown attestations

One file per day: `YYYY/YYYY-MM-DD.json`, its Ed25519 signature `.json.sig` (base64) and an OpenTimestamps proof `.json.ots`.

- **Who**: signed with the key in `PUBLIC_KEY.pem` (`signing_key_id` = first 16 hex of SHA-256 of the key's DER).
- **What**: SHA-256 of `MANIFEST.csv` of this repository (every archived file with its path, rows, bytes and SHA-256) and of the private archive's manifest (digests only, not published).
- **When**: the `.ots` proof anchors the attestation's SHA-256 in Bitcoin through OpenTimestamps calendars. It starts as pending and is upgraded on later days.
- **Order**: `prev` is the SHA-256 of the previous attestation, so the files form a chain. The first file (`baseline: true`) covers everything archived before it.

It shows that these files existed in this form at that time. It does not show that the observations are correct, and it is not a score.

Verify (Node 18+):

```
node -e "const c=require('crypto'),f=require('fs');const d=process.argv[1];console.log(c.verify(null,f.readFileSync(d),c.createPublicKey(f.readFileSync('attest/PUBLIC_KEY.pem')),Buffer.from(f.readFileSync(d+'.sig','utf8').trim(),'base64')))" attest/2026/2026-11-13.json
sha256sum MANIFEST.csv   # compare with public_archive.manifest_sha256 of the day's file (MANIFEST.csv at that commit)
pip install opentimestamps-client && ots verify attest/2026/2026-11-13.json.ots
```
