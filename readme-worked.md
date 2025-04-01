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
more platformio.ini
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
more *.ini
pio run -v
YES, you can make main.cpp on subdir examples/BLE-client*/src
7. connect micro:bit with usb to your pc, then open teraterm or favorite terminal.
baudrate is 115200, other are default (8N1N).
Voila, you see surrounding bles are on the console.
</PRE>

<IMG src="https://github.com/cobwebkanamachi/platform-n-able/blob/mytest-bbcmicro-pio/worked.jpg">
<BR>
Enjoy!
