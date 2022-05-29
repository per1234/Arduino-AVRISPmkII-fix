Arduino-AVRISPmkII-workaround
==========

A **workaround** for [Arduino/#2986](https://github.com/arduino/Arduino/issues/2986). Some people are getting the error message: `avrdude: usbdev_open(): did not find any USB device "usb"` when trying to **Burn Bootloader** using the **AVRISP mkII** programmer under [Arduino](http://arduino.cc) IDE 1.6.x. The problem is that the two avrdude commands are sent without enough delay between them.

This **workaround** adds an **AVRISP mkII Burn Bootloader** option to **Tools > Programmer**. This programmer option causes the **erase** and **bootloader** steps to be done in the first avrdude command so burning the bootloader is accomplished successfully even though the second avrdude command fails as usual.

#### Compatibility

❗ This project is only compatible with Arduino IDE 1.8.12 and older. The support for distributing standalone custom programmer configurations via Arduino boards platforms utilized by this project was lost in Arduino IDE 1.8.13.

You can download Arduino IDE 1.8.12 from this page if needed:

https://www.arduino.cc/en/software/OldSoftwareReleases#arduino-18x

#### Comparison With Alternative **Workaround**
Another **workaround** has been presented in the Arduino Forum by dmjlambert: http://forum.arduino.cc/index.php?topic=345838 here is a comparison of Arduino-AVRISPmkII-workaround vs the dmjlambert **workaround**:
##### Pros
- Doesn't require modification of any Arduino or other hardware core files.
- Doesn't need to be redone every time the Arduino IDE or any hardware core with a platform.txt is updated.
- Doesn't affect any programmer except for AVRISP mkII.

##### Cons
- Burn Bootloader appears to fail even when successful.


#### Installation
There are two options for installing Arduino-AVRISPmkII-workaround:
##### Boards Manager
This installation method requires Arduino IDE version 1.6.4 or greater.
- Open the Arduino IDE.
- Open the **File > Preferences** menu item.
- Enter the following URL in **Additional Boards Manager URLs**: https://per1234.github.io/Arduino-AVRISPmkII-fix/package_per1234_Arduino-AVRISPmkII-fix_index.json.
- Open the **Tools > Board > Boards Manager...** menu item.
- Wait for the platform indexes to finish downloading.
- Scroll down until you see the **Arduino-AVRISPmkII-workaround** entry and click on it.
- If you are using Arduino IDE 1.6.6 then you may need to close **Boards Manager** and then reopen it before the **AVRISP mkII(workaround)** entry will appear.
- Click **Install**.
- After installation is complete close the Boards Manager window.
- If using Arduino IDE previous to v1.6.6 you may need to restart the IDE to make the **AVRISP mkII(workaround)** programmer appear in the **Tools > Programmer** menu.

##### Manual Installation
- Download the Arduino-AVRISPmkII-workaround files here: https://github.com/per1234/Arduino-AVRISPmkII-fix/archive/master.zip.
- Extract the .zip file.
- Copy the extracted folder inside your sketchbook/hardware folder.
- If the Arduino IDE is running then restart it.


#### Usage
##### Burn Bootloader
- Connect the AVRISP mkII to your Arduino.
- Select **Tools > Programmer > AVRISP mkII(workaround)**.
- Select the correct board from **Tools > Board**.
- Click **Tools > Burn Bootloader**.
- The bootloader will be burned to your Arduino but then the avrdude output will fail with the error message `avrdude: usbdev_open(): did not find any USB device "usb"`. This is because the second avrdude command failed as it will do with **Tools > Programmer > AVRISP mkII**, however if you enable **File > Preferences > Show verbose output during: upload**(check) and examine the avrdude output fully you will see that the first command was successful and the bootloader was burned in that command.


#### Contributing
Pull requests or issue reports are welcome! Please see the [contribution rules](https://github.com/per1234/Arduino-AVRISPmkII-fix/blob/master/.github/CONTRIBUTING.md) for instructions.
