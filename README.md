# companion-armbian
A build of Companion that uses Armbian to run on several SBC's
(See also: [companion-satellite-armbian](https://github.com/elliotmatson/companion-satellite-armbian))

## Downloading an image
Ready-made images for a few Orange Pi boards are attached to each [release](https://github.com/elliotmatson/companion-armbian/releases). Flash the `.img.xz` for your board to an SD card with balenaEtcher or Raspberry Pi Imager (both handle `.xz` directly). Companion's web UI is on port 8000.

SSH is enabled. Log in as `root` with password `1234`; you'll be required to set a new password on first login.

## Using this on your own:
This repo uses Github Actions to build Armbian, and then install Companion. It then saves the resulting image file as an artifact for you to write to an SD card. To do this process on your own:

 1. Fork this repository.
 2. Navigate to the `Actions` tab on your fork, and select the action `Build armbian + build companion` on the left pane.
 3. Click `Run Workflow`, and select your board and version of Companion (e.g. `4.3.4`, or `stable` for the latest release).
 4. Run the workflow
After the workflow completes, navigate to the `Summary` tab of that execution, and your image will be attached as `armbian-<board>-companion-<version>.zip`, containing an `.img.xz`.

## How it works
`.github/workflows/build-image.yaml` builds a minimal Ubuntu 26.04 (Resolute) Armbian image for the chosen board from the current [armbian/build](https://github.com/armbian/build) `main` (the exact commit is listed in each release), then uses packer to run the [companion-pi](https://github.com/bitfocus/companion-pi) installer inside it. The same workflow is used by [companion-satellite-armbian](https://github.com/elliotmatson/companion-satellite-armbian).

## Automatic releases
`companion-version.txt` pins the Companion release that gets built into the images, and Renovate keeps it up to date. Whenever it changes on `main`, the `Build Select Boards on Companion Update via Renovate` workflow builds images for a few Orange Pi boards and publishes them as a GitHub release, with Companion's release notes.
