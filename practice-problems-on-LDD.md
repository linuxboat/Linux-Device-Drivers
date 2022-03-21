# Linux-Device-Drivers concept practise and problems

## Practise1:

* Create your own built kernel with your name in EXTRA VERSION option in the Makefile.
* Expected Result: Own built kernel(4.14.180-prabhu) works same as ubuntu kernel(4.15.112)

## Practise2:

* Create your own built kernel with AT keyboard disable as "Disable-keyboard" in EXTRA VERSION option in the Makefile

> 4.14.180-Disable-keyboard
> 
> Disable CONFIG_KEYBOARD_ATKBD option using menuconfig
> 
> Device Drivers -> input device support -> keyboards -> ATKBD (disable)
> 
> #CONFIG_KEYBOARD_ATKBD is not set

* Expected Results: keyboard doesn't work.
### Problems encountered during compilation of Own Build Kernel
> problem1
> 
> >Error ID: BLKCACHE_IOERR(virtual machine stopped at middle of compilation)
> >
> >**solution: check and free virtual machine installed driver**



