## About
[Moonlight for Tizen](https://github.com/ndriqimlahu/moonlight-chrome-tizen) is an open source client for NVIDIA GameStream and [Sunshine](https://github.com/LizardByte/Sunshine).

Moonlight for Tizen allows you to stream your full collection of games from your powerful desktop to your Samsung Smart TV running Tizen OS.

Check out the [Moonlight wiki](https://github.com/moonlight-stream/moonlight-docs/wiki) for more detailed project information, setup guide, or troubleshooting steps.

## Getting Started

Starting with the project, you should first take a look at the required [Prerequisites](https://github.com/ndriqimlahu/moonlight-chrome-tizen-docker#prerequisites) and then follow the [Installation](https://github.com/ndriqimlahu/moonlight-chrome-tizen-docker#installation) instructions in order to successfully install Moonlight on your Samsung Smart TV.

### Prerequisites

Before building this application, you must have [Windows Subsystem for Linux (WSL 2)](https://learn.microsoft.com/en-us/windows/wsl/install-manual) and [Docker Desktop](https://docs.docker.com/desktop/) installed on your computer.

Also, you should run "Docker Desktop" before proceeding further and it is also recommended to close any software or application that requires high CPU and memory resources, because "Docker Desktop" will take high resources during use.

### Installation
1. Download the [Dockerfile](https://github.com/ndriqimlahu/moonlight-chrome-tizen-docker/blob/main/Dockerfile) and save it in the "Downloads" folder, then you should remove any extensions from the `Dockerfile` and just leave it without extensions.
2. Open `Windows PowerShell` or a similar program depending on your OS, then change directory to where you downloaded the `Dockerfile`, so for example if you downloaded the file in the "Downloads" folder, then you should enter the following command to go on that path.
	```
	cd .\Downloads\
	```
3. Enable the "Developer mode" in your "Samsung Smart TV" (If you need more detailed instructions, see the official [Samsung guide](https://developer.samsung.com/smarttv/develop/getting-started/using-sdk/tv-device.html)):
	- Go to the `Apps` panel.
	- Press `12345` on the remote and a dialog should popup.
	- Set `Developer mode` to `On` and fill in the `Host PC IP` field which is the `IP Address` of your PC, then click the `OK` button to close the dialog.
	- Restart the TV by holding the power button for 2 seconds as instructed by the new dialog popup, then again go to the `Apps` panel.
	- Depending on your model, a `DEVELOP MODE` or similar message will appear in the `Apps` panel at the top of the screen.
4. After that, in `Windows PowerShell`, enter the following command to build the application within a "Docker" image:
	```
	docker build -t moonlight-tizen . --no-cache
	```
	- This operation may take a while, please be patient.
 	> Note: If you are running "Docker" on a "Mac" with a silicon chip (M1/M2 etc), then you need to change the first line in the `Dockerfile` to `FROM --platform=linux/amd64 ubuntu:22.04` before building the application to ensure compatibility.
5. After that, in `Windows PowerShell`, follow the steps below to install the application on your TV:
	- Enter the following command to run and enter a container:
	 ```
	 docker run -it --rm moonlight-tizen
	 ```
	- Next, enter the following command to connect to your "Samsung Smart TV" over "Smart Development Bridge":
	 ```
	 sdb connect YOUR_TV_IP
	 ```
   	> Note: Replace `YOUR_TV_IP` with `IP Address` of your TV.
	- Next, enter the following command to confirm that you are connected, then take note of the "Device ID":
	 ```
	 sdb devices
	 ```
   	> Note: Just to clarify "Device ID" will be the last column, something like `UE55AU7172UXXH`.
	- Next, enter the following command to install the package:
	 ```
	 tizen install -n Moonlight.wgt -t YOUR_DEVICE_ID
	 ```
   	> Note: Replace `YOUR_DEVICE_ID` with `Device ID` of your TV.
 	- After that, Moonlight should now appear in your `Recent Apps` or similar page on your "Samsung Smart TV".
	- Next, enter the following command to exit the container:
	 ```
	 exit
	 ```
	- Finally, enter the following command to remove the "Docker" image:
	 ```
	 docker image rm moonlight-tizen
	 ```
   	> Note: At the end you can enter the `exit` command to close the `Windows PowerShell` window.
6. Disable the "Developer mode" in your "Samsung Smart TV":
	- Go to the `Apps` panel.
	- Press `12345` on the remote and a dialog should popup.
	- Set `Developer mode` to `Off` and then click the `OK` button to close the dialog.
	- Restart the TV by holding the power button for 2 seconds as instructed by the new dialog popup, then again go to the `Apps` panel.
	- Depending on your model, a `DEVELOP MODE` or similar message will disappear from the `Apps` panel at the top of the screen.
7. Now you can launch Moonlight on your TV, then add your host computer and enjoy the high quality streaming experience.

### Updating

1. Before updating the Moonlight app, you must delete the installed Moonlight app that you already have on your Samsung Smart TV to prevent errors during the update.
2. Now, whenever you want to install an updated version of Moonlight on your Samsung Smart TV, you need to follow the [Installation](https://github.com/ndriqimlahu/moonlight-chrome-tizen-docker#installation) instructions in order to successfully install the updated version of Moonlight on your Samsung Smart TV.

### Testing

> Note:  FOR DEVELOPERS ONLY.
1. Fork and clone the `moonlight-chrome-tizen` repository.
2. Open `Windows PowerShell` or a similar program depending on your OS, then change directory to where you cloned the repository, then use the `Dockerfile` from source code folder, so for example you should enter the following command to go on that path.
	```
	cd C:\repo\moonlight-chrome-tizen\
	```
3. After that, you can continue the [Installation](https://github.com/ndriqimlahu/moonlight-chrome-tizen-docker#installation) instructions from the third step in order to successfully install the Moonlight patch version on your Samsung Smart TV.
4. So remember whenever you make changes, add features, fix bugs, and other developments, it is recommended to test on your device first before creating a pull request or pushing an update.

### FAQ

1. How can I find out what TV model I have?
- Using your Samsung Smart TV remote, follow these steps: `Settings` -> `Support` -> `About This TV`.

2. Which supported controllers can I use on my TV?
- You can use the most popular Bluetooth or USB-wired controllers: Microsoft Xbox Series X/S controllers, Xbox One controller, Xbox 360 controller, Xbox Elite Wireless controller Series 2, Xbox Adaptive controller, PlayStation DualShock 4 and DualSense controllers, Amazon Luna Wireless controller, NVIDIA Shield controller, Logitech F310, F510 and F710 controllers, PowerA MOGA XP5-X Plus Bluetooth controller, Joytron CYVOX DX.

3. Having trouble with unsupported controllers on my TV?
- If you use any Bluetooth or USB 2.0 game controllers other than those mentioned in the previous question, then unfortunately you may encounter problems such as unresponsive Guide and D-PAD buttons, Y and X buttons switching, vibration rumble motor which does not work and other controller issues.

4. How do I connect my Bluetooth controller to my TV?
- Using your Samsung Smart TV remote, follow these steps: `Settings` -> `Connection` -> `External Device Manager` -> `Input Device Manager` -> `Bluetooth Device List` -> Then pair your controller.

5. How can I test the functionality of the controller on my TV?
- To test the functionality of the controller on Samsung Smart TV, you can use the [GamepadChecker](https://developer.samsung.com/smarttv/accessory/gamepad.html) application, please visit the above link and follow all the instructions in the "Testing Gamepad Functionality" section to download and install the app on your Samsung Smart TV.

6. How can I pin the Moonlight app icon to the home screen for easy access?
- Once you install the Moonlight app, hover over the app icon and long press the "OK" button on your TV remote. Then select `Add to Home`. Use the cursor to move the icon where you want it to be in the app launcher row on the home screen.

## Changelogs

See the [CHANGELOG](https://github.com/ndriqimlahu/moonlight-chrome-tizen/blob/samsung_wasm/CHANGELOG.md) file for more information about the changes for each version of this project.

## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this project better, then feel free to fork the repo, create a pull request or open an issue.

Also, if you liked the project or found it useful, don't forget to give the project a star!

## License

This project is licensed under the `GNU General Public License v3.0`. See the [LICENSE](https://github.com/ndriqimlahu/moonlight-chrome-tizen/blob/samsung_wasm/LICENSE) file for more information.

## Credits
- Moonlight for Chrome OS is developed and maintained by [Moonlight Developers](https://github.com/moonlight-stream/moonlight-chrome)
- Moonlight for Tizen is based on Chrome OS version which was then adapted and powered by [Samsung Developers](https://github.com/SamsungDForum/moonlight-chrome)
- Support files and Dockerfile have been adapted by [jellyfin](https://github.com/jellyfin/jellyfin-tizen) and [babagreensheep](https://github.com/babagreensheep/jellyfin-tizen-docker)
- Dockerfile have been readapted by [pablojrl123](https://github.com/pablojrl123/moonlight-tizen-docker)
- Content files and Dockerfile have been readapted by [KyroFrCode](https://github.com/KyroFrCode/moonlight-chrome-tizen) & [KyroFrCode](https://github.com/KyroFrCode/moonlight-chrome-tizen-docker)
