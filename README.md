# arduino-pico
Raspberry Pi Pico Arduino core, for all RP2040 boards

This is a port of the RP2040 (Raspberry Pi Pico processor) to the Arduino ecosystem.

It uses a custom toolset with GCC 10.2 and Newlib 4.0.0, not depending on system-installed prerequisites.  https://github.com/earlephilhower/pico-quick-toolchain

There is automated discovery of boards in bootloader mode, so they show up in the IDE, and the upload command works using the Microsoft UF2 tool (included).

# Installing via Arduino Boards Manager
Open up the Arduino IDE and go to File->Preferences.

In the dialog that pops up, enter the following URL in the "Additional Boards Manager URLs" field:
https://github.com/earlephilhower/arduino-pico/releases/download/0.9.0/package_rp2040_index.json
![image](https://user-images.githubusercontent.com/11875/111917251-3c57f400-8a3c-11eb-8120-810a8328ab3f.png)

Hit OK to close the dialog.

Go to Tools->Boards->Board Manager in the IDE

Type "pico" in the search box and select "Add":
![image](https://user-images.githubusercontent.com/11875/111917223-12063680-8a3c-11eb-8884-4f32b8f0feb1.png)

# Installing via GIT
To install via GIT (for latest and greatest versions):
````
mkdir -p ~/Arduino/hardware/pico
git clone https://github.com/earlephilhower/arduino-pico.git ~/Arduino/hardware/pico/rp2040
cd ~/Arduino/hardware/pico/rp2040
git submodule init
git submodule update
cd pico-sdk
git submodule init
git submodule update
cd ../tools
python3 ./get.py
`````


# Status of port
Lots of things are working now!
* digitalWrite/Read (basic sanity tested)
* shiftIn/Out (tested using Nokia5110 https://github.com/ionpan/Nokia5110)
* SPI (tested using SdFat 2.0 https://github.com/greiman/SdFat ... note that the Pico voltage regulator can't reliably supply enough power for a SD Card so use external power, and adjust the `USE_SIMPLE_LITTLE_ENDIAN` define in `src/sdfat.h` to 0)
* analogWrite/PWM (tested using Fade.ino)
* tone/noTone (using IRQ generated waveform)
* Wire/I2C (tested using DS3231 https://github.com/rodan/ds3231)
* EEPROM (tested examples)
* USB Serial(ACM) w/automatic reboot-to-UF2 upload)
* Hardware UART
* Servo (basic waveform testing, disables/re-enables without any short pulses)

The RP2040 PIO state machines (SMs) are used to generate jitter-free:
* Servos
* Tones

# Contributing
If you want to contribute or have bugfixes, drop me a note at <earlephilhower@yahoo.com> or open an issue/PR here.

-Earle F. Philhower, III
 earlephilhower@yahoo.com
