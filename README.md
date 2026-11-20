# YouDash IPA Build

Automated build wrapper for [YouDash](https://github.com/sa4hnd/YouDash), the native YouTube integration for Apple CarPlay.

This repository builds the open-source CarPlay integration module from the upstream source and publishes it as a GitHub Actions artifact. It does **not** include Google's proprietary YouTube app or a decrypted YouTube/YouMod IPA.

## Build with GitHub Actions

1. Open **Actions**.
2. Select **Build YouDash module**.
3. Select **Run workflow**.
4. Download the `YouDash-module` artifact after the job completes.

The workflow uses macOS, Xcode's iPhoneOS SDK, and Python to run the upstream `--compile-only` build. The output is `YouTubeCarPlay.dylib`.

## Package an IPA

To create an unsigned IPA, follow the upstream [build guide](https://github.com/sa4hnd/YouDash/blob/main/docs/BUILD.md). You need a compatible, decrypted YouTube + YouMod IPA that you are authorized to modify. The documented baseline is YouTube 21.42.4 + YouMod 2.0.0.

For device installation, you also need your own authorized Apple signing certificate, provisioning profile, registered device, and the required CarPlay capability. This repository does not provide or bypass Apple entitlements, signing, or proprietary app assets.

## Upstream

- Source: https://github.com/sa4hnd/YouDash
- Build instructions: https://github.com/sa4hnd/YouDash/blob/main/docs/BUILD.md
- License: GPL-3.0 (see upstream license and notices)

The upstream project remains the source of truth. This repository is an automated build wrapper, not an independently maintained copy.
