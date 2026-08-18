# Replica releases

Signed release artifacts for the **Replica** desktop app.

There is no source code in this repository, and there never should be. It
exists for one reason: the app checks for updates from a machine that has no
GitHub credentials, and GitHub only serves release downloads from a *private*
repository to authenticated users. Hosting the artifacts here is what lets an
installed copy fetch its own updates.

## What is published here

Each release carries:

| Asset | What it is |
|---|---|
| `Replica.io-Installer.exe` | The installer |
| `Replica-Updater.exe` | The small helper that applies an update in place |
| `version.json` | An Ed25519-signed manifest: version, download URL, SHA-256 |

## Why publishing these publicly is safe

- **`version.json` is signed, not trusted.** The app carries the public half of
  the signing key compiled into the binary and verifies the signature offline.
  Anyone can read this manifest; nobody without the private key can write one
  the app will accept. Replacing a file here does not get code onto anyone's
  machine.
- **The installer is checked against the manifest.** The app re-verifies the
  SHA-256 of what it downloaded before running it.
- **The binary is obfuscated, and the source is not here.**
- **Downloading it gets you a login screen.** The app requires a Supabase
  account and a paid entitlement; the private half of everything that matters
  lives on the account server.

## How it gets here

Automatically, from CI in the private source repository, on every push to its
`main`. Nothing is uploaded by hand.
