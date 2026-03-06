**German/Deutsch**: https://github-com.translate.goog/maldieve/Anno1800UXEnhancer?_x_tr_sl=auto&_x_tr_tl=de&_x_tr_hl=de&_x_tr_pto=wapp

[![Build](https://github.com/maldieve/Anno1800UXEnhancer/actions/workflows/build.yml/badge.svg)](https://github.com/maldieve/Anno1800UXEnhancer/actions/workflows/build.yml)

# Usage

## Statistics Extractor
[![Tutorial](https://raw.githubusercontent.com/NiHoel/Anno1800Calculator/master/CalculatorExtractionScreenshot.png)](https://youtu.be/k4WmgEIkp4s)

- [one-time setup] download, install (and reboot your computer afterwards): [vc_redist](https://support.microsoft.com/en-gb/help/2977003/the-latest-supported-visual-c-downloads)
- run the Server.exe from the [zip archive](https://github.com/maldieve/Anno1800UXEnhancer/releases/latest/) which should open a command window and might require administrator rights
- run [Anno1800Calculator](https://github.com/NiHoel/Anno1800Calculator/releases/latest/) from local file (if not done already)
- run Anno 1800
- open the statistic menu (population to update number of houses, finance to update number of factories, production to update productivity)
- alternatively, one can update the population from the overlay of the HUD (not recommended)
- [Tutorial](https://youtu.be/k4WmgEIkp4s)


## Rerollbot
[![Tutorial](https://img.youtube.com/vi/pPx0_A10G2Q/0.jpg)](https://youtu.be/pPx0_A10G2Q)

- [one-time setup] download, install (and reboot your computer afterwards): [vc_redist](https://support.microsoft.com/en-gb/help/2977003/the-latest-supported-visual-c-downloads)
- Run UXEnhancer.exe
- Edit the counters to specify how many times you want to buy that item (9999 is the maximum count and equivalent to infinity).
- (Optional) Set a cost limit. Rerolls are only performed if the costs are below this limit. A limit of 0 means no limit.
- Open the trade menu of a trader that sells one of the items you want. The bot will start buying / rerolling automatically
- Hit 'Esc' to pause the bot and close the window
- [Tutorial](https://youtu.be/yOkjKXnUFAw)
- Thanks to [Veraatversus](https://github.com/Veraatversus) for adapting the AssetViewer

## Advices to further speed up rerolling
1. Close other programs that consume CPU.
2. Assign UXEnhancer.exe a task priority of "high".
3. Move the game to the SSD drive.
4. Lower graphics settings.
5. Set reroll cost (max.) to 0 (unbounded)

In general, 2 rerolls per second are a really good value and 3 rerolls per second the absolute maximum.

## Run the calculator remotely
The server needs to be run on the same computer as Anno. But the calculator can be run on a mobile device (laptop, smartphone, ...)
One has to ensure that server and client can communicate:

  1. The desktop computer must be reachable from the mobile device (e.g. be in the same network, inter device communication is enabled by the router and the mobile device can ping the desktop computer)
  2. The port 8000 must be open for incoming traffic (and responses). Check windows defender and / or the antivirus software
  3. Search for 'http://localhost:8000/AnnoServer/Population' in `dist\calculator.bundle.js` and replace localhost by the IP address of the desktop computer
  4. Open a terminal in administrator mode, navigate to the folder containing the server and enter: ".\Server.exe -h " followed by the ip address of the **desktop** computer (do not add http or anything else)
  
Connectivity can be checked by entering the url displayed in the terminal into the browser of the mobile device. Then a log "request received" should appear in the terminal.


# Troubleshooting
In case **vcruntime140_1.dll** is missing, download the vc_redist from [https://support.microsoft.com/en-gb/help/2977003/the-latest-supported-visual-c-downloads](https://support.microsoft.com/en-gb/help/2977003/the-latest-supported-visual-c-downloads)

In case nothing happens, make sure:
- the ingame text language and the language of the calculator/bot config are identical
- the values to be read are not covered by something else (overlay, external program, etc.; basically things you would see when running a screen capturing program)
- The window mode of the game is set to 'windowed full screen'
- Disable XBOX DVR 
- Set the gamma value of the game (graphics settings) to its default (center position of the slider)
- Disable Windows HD Colour (skip this point if you do not know what this is)
- (Statistics Extractor) the correct island is selected in the statistics screen
- (Statistics Extractor) the island has a long (> 8 letters) name composed from standard letters (A-Za-z) and with other islands as few characters in common as possible
  - NEGATIVE example: "Múa-1" and "Múa-2": Too short, non standard letter ú and both names only differ in one letter
- (Statistics Extractor) in the center of the statistics menu the selected entry is fully visible

- (UXEnhancer) Some items have identical prices and icons. In such cases wrong items might be bought or several counters decremented although only one item was bought.
- If the game window is not found (e.g. you stream it from a cloud gaming platform), then you can specify the title of the window manually. Enter ".\UXEnhancer.exe -w " (repectively ".\Server.exe -w ") followed by the title of the window in quotation marks. The string you specify is interpreted as a regular expression. This means that '.' is a wildcard and "()[]*\" are reserved characters.

**If you encounter any bug, feel free to contact me (e.g. open an issue) and if possible perform the following steps**
- Open the program in the console with verbose option:
- Shift + right click on folder containing the exe file -> Open PowerShell Window -> Enter ".\UXEnhancer.exe -v" or ".\CalculatorServer.exe -v" (without the quotes)
- Configure and open the store / Open the statistics screen or where the bug occurred
- Close the program without closing any dialog in Anno
- Send me the console output + debug_images (+ UXEnhancerConfig.json - if the rerollbot is concerned)


# Use prebuild binaries
- download the latest release from https://github.com/maldieve/Anno1800UXEnhancer/releases/latest/
- extract the archive to any location you desire

# Build it yourself 
## Requirements
- Git-installation (e.g. https://git-scm.com/download/win)
- Visual Studio 2019 or higher (https://visualstudio.microsoft.com/) with the **C++ Desktop development** workload and the **English language pack** installed
	
## Build instructions
```bat
git clone --recurse-submodules https://github.com/maldieve/Anno1800UXEnhancer.git
cd Anno1800UXEnhancer
SETUP.bat
```

`SETUP.bat` will bootstrap vcpkg and set up directory links. After that, install the required libraries with vcpkg (all commands run from the repository root):

```bat
cpp\vcpkg\vcpkg.exe install ^
  boost-property-tree:x64-windows ^
  boost-algorithm:x64-windows ^
  boost-filesystem:x64-windows ^
  boost-functional:x64-windows ^
  tesseract:x64-windows ^
  "cpprestsdk[core]:x64-windows" ^
  "opencv4[png]:x64-windows" ^
  "opencv4[jpeg]:x64-windows"
```

Then open `cpp\visual studio\UXEnhancer.sln` in Visual Studio, select **Release | x64** and build.

> **Tip:** A GitHub Actions workflow (`.github/workflows/build.yml`) is included and will build the solution automatically on every push, producing ready-to-use artifacts.

## Troubleshooting 
- copy, move, rename errors during installation: make sure that vcpkg resides on a short path (e.g. access the folder via a drive letter)
- vcpkg error "Please install the English language pack. Could not locate a complete toolset."
  → go to Visual Studio Installer → Visual Studio Community → Modify → Language Packs → select **English** → click **Modify**
- if Visual Studio is not installed on `C:\Program Files (x86)`, OpenGL (part of OpenCV) might fail to build.
  Possible fix: https://github.com/Microsoft/vcpkg/issues/4377
  or reinstall the Windows SDK to the default location.

- To update `ui_texts.json`, place the contents from `Anno 1800/maindata/data2.rda//data/config/gui/` in `cpp/visual studio/CalculatorServer/x64/Release/texts` and delete `ui_texts.json`. Running the server in release mode will recreate it from the source files.

