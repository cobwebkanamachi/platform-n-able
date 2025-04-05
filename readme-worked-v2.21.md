I got micro:bit v2.21 worked with this repo yesterday (2025/04/05).
<PRE>
brief procedures:
1. clone this repo
   git clone reponame --recursively
3. replace two platformio.ini with this repo's one(NOT INCL. THIS REPO, PLS PASTE BELLOW).
  --- CUT HERE ---
  $pwd
  /mnt/c/users/user/Documents/platformio/Projects/platform-n-able-v2
  [env:bbcmicrobit_v2]
  platform = https://github.com/h2zero/platform-n-able.git@^1.0.0
  framework = arduino
  lib_deps = https://github.com/h2zero/NimBLE-Arduino.git@^2.1.1
  board = bbcmicrobitv2
  --- CUT HERE ---
  $pwd
  /mnt/c/users/user/Documents/platformio/Projects/platform-n-able-v2/examples/BLE-client-test 
  [env]
  platform = n-able
  framework = arduino
  monitor_speed=115200
  [common]
  lib_deps = h2zero/NimBLE-Arduino@^1.4.3
  build_flags =
   '-DCONFIG_NIMBLE_CPP_LOG_LEVEL=0'
   '-DCONFIG_BT_NIMBLE_ROLE_PERIPHERAL_DISABLED'
   '-DCONFIG_BT_NIMBLE_ROLE_BROADCASTER_DISABLED'
  [env:bbcmicrobitv2]
  board = bbcmicrobitv2
  lib_deps = ${common.lib_deps}
  build_flags = ${common.build_flags}
4. pio run -v (project top)
  this do not makes executable. next proc. needed.  
5. pio run -v (under examples)
  on this proc., firmware.elf made.
6. firmware.elf made
7. openocd + gdb -> file firmware.elf & load & continue
8. you get grin.
   baud : 115200, 8N1S(same as original, if not matched, that's my mistake sorry)</PRE>
<BR>
<img src="https://github.com/cobwebkanamachi/platform-n-able/blob/mytest-bbcmicro-pio/workedV221-1.jpg">
<img src="https://github.com/cobwebkanamachi/platform-n-able/blob/mytest-bbcmicro-pio/workedV221-2.jpg">

Enjoy!
<pre>
footnote:
I test on Arduino IDE, Nimble-Arduino and n-able-arduino. I saw something too similar with this repo.
And g++ not compiled them, so I tested this repo with arduino setting in platformio.ini. it succeed.
Why I did on Arduino IDE, that is hinted usb uart not worked simply build this for v2.21.
I did not know V2.21 has changed USB Controller chip with previous versions of bbc:micro.
I saw usb uart not worked, so I seek difference with v2.21 and previous versions.
And Arduino and Make Code perhaps already adjust usb controller change.
So I did Arduino experiment and back to pio.
</pre>
