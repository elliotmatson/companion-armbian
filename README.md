# companion-armbian
A build of Companion that uses Armbian to run on several SBC's
(See also: [companion-satellite-armbian](https://github.com/grace-bible/companion-satellite-armbian))

## Using this on your own:
This repo uses Github Actions to build Armbian, and then install Companion. It then saves the resulting image file as an artifact for you to write to an SD card. To do this process on your own:

 1. Fork this repository.
 2. Navigate to the `Actions` tab on your fork, and select the action `Build armbian + build companion` on the left pane.
 3. Click `Run Workflow`, and select your board and version of Companion (e.g. `4.3.4`, or `stable` for the latest release).
 4. Run the workflow
After the workflow completes, navigate to the `Summary` tab of that execution, and your image file will be attached as `armbian-<board>-companion-<version>.zip`

## Automatic releases
`companion-version.txt` pins the Companion release that gets built into the images, and Renovate keeps it up to date. Whenever it changes on `main`, the `Build Select Boards on Companion Update via Renovate` workflow builds images for a few Orange Pi boards and publishes them as a GitHub release.
