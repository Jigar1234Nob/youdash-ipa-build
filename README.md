# YouDash IPA Build

Build an unsigned, sideloadable IPA package for [YouDash](https://github.com/sa4hnd/YouDash), the native YouTube integration for Apple CarPlay.

This repository automates the upstream packaging process. It does **not** host or provide Google's proprietary YouTube app, YouMod binaries, decrypted IPAs, Apple certificates, or provisioning profiles. You must supply an input IPA that you are authorized to modify.

## What you need

- A compatible, **decrypted** YouTube + YouMod IPA. The upstream documented baseline is YouTube 21.42.4 + YouMod 2.0.0.
- A direct HTTPS download URL for that IPA. Store it as a GitHub Actions repository secret named `YOUDASH_INPUT_IPA_URL`. Do not commit the IPA or its URL to this repository.
- GitHub Actions enabled for this repository.

To add the secret, open **Settings → Secrets and variables → Actions → New repository secret**. Set the name to `YOUDASH_INPUT_IPA_URL` and the value to the direct HTTPS download URL for your own compatible IPA. The URL must be accessible to GitHub Actions without an interactive login. Keep it private.

## Build an IPA

1. Open the **Actions** tab.
2. Select **Build YouDash unsigned IPA**.
3. Choose **Run workflow**.
4. Keep the default bundle ID or enter one you control.
5. Keep the default reported version unless the upstream compatibility guide tells you otherwise.
6. Start the workflow and wait for it to finish.
7. Open the completed run and download **YouDash-unsigned-IPA**.
8. Extract the downloaded artifact. It contains the unsigned `.ipa` and `SHA256SUMS.txt`.

## Install with Scarlet

1. Download the artifact on your iPhone and extract it if iOS has not already done so.
2. Open the `.ipa` in Scarlet and use Scarlet's import/sign/install flow.
3. If Scarlet rejects the package, check that the IPA downloaded completely and that your signing method supports the app's required capabilities.

The workflow intentionally produces an **unsigned** IPA. Scarlet (or another sideloading signer) must sign it before iOS will install it. This build workflow does not receive Apple account credentials or signing certificates.

## Important CarPlay limitation

Installing the app does not automatically make YouDash work on a CarPlay screen. Upstream documents that the app requires the `com.apple.developer.carplay-video` entitlement to be authorized by the signing profile. Ordinary sideloading, including re-signing with Scarlet, cannot grant an entitlement that Apple has not authorized for that profile. A profile without that capability may let the app install while the CarPlay video integration remains unavailable.

Use this only while parked and follow local laws and your vehicle's restrictions.

## Upstream documentation

- [YouDash source](https://github.com/sa4hnd/YouDash)
- [Upstream build guide](https://github.com/sa4hnd/YouDash/blob/main/docs/BUILD.md)
- [Upstream compatibility notes](https://github.com/sa4hnd/YouDash/blob/main/docs/COMPATIBILITY.md)
- [GPL-3.0 license and notices](https://github.com/sa4hnd/YouDash/blob/main/LICENSE)

This repository is a build wrapper. The upstream project remains the source of truth for code, compatibility, and build requirements.
