# Visual Studio Code for Arduino

## Introduction

[Visual Studio Code](https://code.visualstudio.com/download) is a good alternative the the Arduino IDE:
- It supplies the needed functionality to code, compile and upload Arduino programs
- It works on 64-bit ARM, which Arduino have not supplied an official package
- Lots of tools and aids to help with development, not just in C/C++, but also Markdown, JSON, etc

You can grab the package from the direct [.deb Arm64](https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-arm64) link - this will work on any Debian-based Linux OS.

Once the package downloaded, it can be installed as follows:
```
sudo dpkg -i ~/Downloads/code_1.85.2-1705560689_arm64.deb
```

## Initial Setup

Once installed, there should be a "Visual Studio Code" entry under "Development" if you are running a desktop with auto-populated menus.

Open it up, then open **Extensions** view (blocks icon) or go to **View->Extensions** in the menu.

In the search bar, type `arduino` and click the **Install** button next to the official Microsoft extension.

After installing you may be recommended for **C/C++ Extension Pack** - accept this to get assistance when coding.

Also you will be prompted to use the Arduino CLI over the Arduino IDE - click **Use bundled arduino-cli**.

## Board Installation

Hit **Ctrl+Shift+P** - this allows the developer to both search for and execute commands, some extension specific.

Search for **Arduino: Board Manager** and execute it. 

If an Arduino is to be used, search the results and select the appropriate package here that contains the board and hit **Install** next to it.

If the board is not seen or associated with the Arduino project (e.g. Raspberry Pi, Adafruit, Xiao, SparkFun, Waveshare, etc), follow this process:
1. Grab the package.json URL, probably from the chip-vendor. For example, here are some common ones:
    - [arduino-pico - for RP2040](https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json)
    - [arduino-esp32 - for ESP32](https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json)

2. Open **Extensions**, click the cog/gear icon (AKA "Manage") and select **Extension Settings** from the dropdown.

3. Under **Arduino: Additional Urls**, click the **Add Item** button, paste in the respective `package.json` URL into the text box and hit the **OK** button.

4. Close Visual Studio Code and reopen.

5. Use **Ctrl+Shift+P** to find the **Arduino: Board Manager** command

6. Something like the following should be seen in the **OUTPUT** section at the bottom of the screen:
```
[Starting] Update package index files...
dummy

Downloading index: package_index.tar.bz2 0 B / 56.97 KiB    0.00%
Downloading index: package_index.tar.bz2 downloaded

Downloading index: package_esp32_index.json 0 B / 147.15 KiB    0.00%
Downloading index: package_esp32_index.json downloaded
[Done] Updated package index files.
```

7. If all is good, search for the new package (packages are not installed by default) and hit the Install button next to the appropriate version to be used. This will download all the appropriate compilers, boards, programmers, etc.

8. Close and reopen Visual Studio Code.

## Board Configuration

At the bottom of the screen is **Select Board Type**. This opens up **Arduino Board Configuration**. Select a board from the dropdown.

Once done, there may be options appearing after a second or so, immediately below the board selection, specific to that board. If so, select the appropriate options. If not, particularly if a AVR board is in use, the following options at the bottom of the screen may be relevant:
- *Select Programmer* - what is method used to program the microcontroller
- *Select Serial Port* - what should the programmer use to access the microcontroller

NOTE: It appears that the Arduino Extension in Visual Studio Code does not recognise custom hardware configurations held in `*.local.txt` files. Instead, the contents of these files will need to be appended to the existing variants of `board.txt`, `platform.txt` and `programmer.txt`.

## Testing
Selecting a valid board will allow **Arduino: Examples** to be exposed for that board.

Open any example deemed fit to test the board in question and then run:
- *Arduino: Verify* (Ctrl+Alt+R)
- *Arduino: Upload* (Ctrl+Alt+U)
