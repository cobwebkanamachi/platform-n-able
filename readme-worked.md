<PRE>
I test build client for micro:bit (v1.3B) with pio.
Finally made firmware.elf of bbcmicro(v1.3B) and run it successfull.
Build procedures are bellow:
1. git clone
git clone https://github.com/h2zero/platform-n-able --recursive
2. pio init
platformio project init
3. check and write platformio.ini
put this repo's platform.io to your project dir of top.
My case was : /mnt/c/Users/user/Documents/PlatformIO/Projects/platform-n-able
-- cut here --
[env:bbcmicrobit]
platform = https://github.com/h2zero/platform-n-able.git@^1.0.0
framework = arduino
lib_deps = h2zero/NimBLE-Arduino@^1.4.0
board = bbcmicrobit
-- cut here --
save file, then more platformio.ini (check).
4. if you did not have installed scons for your python3, pls install it.
pio run -v
pip3 install scons
pio run -v
5. if pio run -v failed, perhaps subdirs did not make copied, so hand copy pls.
cp -r ./builder /home/cobweb/.platformio/platforms/n-able/builder/
cp -r ./examples /home/cobweb/.platformio/platforms/n-able/builder/
cp -r ./boards /home/cobweb/.platformio/platforms/n-able/builder/
cp -r ./misc* /home/cobweb/.platformio/platforms/n-able/builder/
cp -r ./tools /home/cobweb/.platformio/platforms/n-able/builder/
6. then, setup and loop were not build, that is because main.cpp is on subdir.
pls do this bellow.
cd examples//BL*client*/src
cd .pio/build/bbcmicrobit/
nm libFrameworkArduino.a |grep loop
nm libFrameworkArduino.a |grep setup
find . -name main.cpp.o -print
nm ./.pio/build/bbcmicrobit/FrameworkArduino/main.cpp.o
cd examples/BLE-client*/src
more *.ini -> you have no need to write platformio.ini (prewrote here).
pio run -v
YES, you can make main.cpp on subdir examples/BLE-client*/src
7. connect micro:bit with usb to your pc, then open teraterm or favorite terminal.
baudrate is 115200, other are default (8N1N).
Voila, you see surrounding bles are on the console.
</PRE>

<IMG src="https://github.com/cobwebkanamachi/platform-n-able/blob/mytest-bbcmicro-pio/worked.jpg">
<BR>
<PRE>
Addendum: 
Binaries made were bellow( I stopped on the way, bellow are not all).
[cobweb@BLE-client-test]$find . -name "firmware.elf" -print
./.pio/build/adafruit_clue_nrf52840/firmware.elf
./.pio/build/adafruit_cplaynrf52840/firmware.elf
./.pio/build/adafruit_feather_nrf52832/firmware.elf
./.pio/build/adafruit_feather_nrf52840/firmware.elf
./.pio/build/adafruit_feather_nrf52840_sense/firmware.elf
./.pio/build/adafruit_itsybitsy_nrf52840/firmware.elf
./.pio/build/bbcmicrobit/firmware.elf
./.pio/build/bbcmicrobitv2/firmware.elf
./.pio/build/bluey/firmware.elf
./.pio/build/bluz_dk/firmware.elf
./.pio/build/BT5032A_TB/firmware.elf
./.pio/build/BT5040/firmware.elf
./.pio/build/calliope_mini/firmware.elf
./.pio/build/generic_nrf51822_xxaa/firmware.elf
./.pio/build/generic_nrf51822_xxac/firmware.elf
./.pio/build/generic_nrf52810/firmware.elf
./.pio/build/generic_nrf52832/firmware.elf
./.pio/build/generic_nrf52833/firmware.elf
./.pio/build/generic_nrf52840/firmware.elf
./.pio/build/hackaBLE/firmware.elf
./.pio/build/hackaBLE_v2/firmware.elf
./.pio/build/ng_beacon/firmware.elf
./.pio/build/nrf51_dk/firmware.elf
./.pio/build/nrf51_dongle/firmware.elf
./.pio/build/nrf52832_dk/firmware.elf
./.pio/build/nrf52833_dk/firmware.elf
./.pio/build/nrf52840_dk/firmware.elf
./.pio/build/nrf52840_dongle/firmware.elf
./.pio/build/oshchip/firmware.elf
./.pio/build/redbear_blenano/firmware.elf
./.pio/build/redbear_blenano2/firmware.elf
./.pio/build/redbear_blend2/firmware.elf
./.pio/build/redbear_nRF51822/firmware.elf
(stoppped by me)
</PRE>
Enjoy!
