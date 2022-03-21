Practise1:

Create your own built kernel with your name in EXTRA VERSION option in the Makefile.
Expected Result: Own built kernel(4.14.180-prabhu) works same as ubuntu kernel(4.15.112)

Practise2:

Create your own built kernel with AT keyboard disable as "Disable-keyboard" in EXTRA VERSION option in the Makefile

4.14.180-Disable-keyboard
Disable CONFIG_KEYBOARD_ATKBD option using menuconfig
Device Drivers -> input device support -> keyboards -> ATKBD (disable)
#CONFIG_KEYBOARD_ATKBD is not set

Expected Results: keyboard doesn't work.