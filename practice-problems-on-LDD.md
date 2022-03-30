# Linux-Device-Drivers concept practice and problems

## Linux Device Drivers Development Environment Setup

### Practice1:

* Create your own built kernel with your name in EXTRA VERSION option in the Makefile.
* Expected Result: Own built kernel(4.14.180-prabhu) works same as ubuntu kernel(4.15.112)

### Practice2:

* Create your own built kernel with AT keyboard disable as "Disable-keyboard" in EXTRA VERSION option in the Makefile

> 4.14.180-Disable-keyboard
> 
> Disable CONFIG_KEYBOARD_ATKBD option using menuconfig
> 
> Device Drivers -> input device support -> keyboards -> ATKBD (disable)
> 
> #CONFIG_KEYBOARD_ATKBD is not set

* Expected Results: keyboard doesn't work.

#### Problems encountered during compilation of Own Build Kernel

> **Problem1**
> 
>>**Error ID: BLKCACHE_IOERR(virtual machine stopped at middle of compilation)**
>>
>>**Solution:** check and free virtual machine installed driver
>>
> **Problem2**
> 
>>**Attempting to compile kernel yields a certification error(Makefile:1726: recipe for target 'certs' failed)**
>>
>>**Solution:** In the .config file copied from /boot find and comment out the lines
>> 
>>CONFIG_SYSTEM_TRUSTED_KEYS
>> 
>>CONFIG_MODULE_SIG_KEY
>>
> **Problem3**
> 
>>**BTF: .tmp_vmlinux.btf: pahole (pahole) is not available Failed to generate BTF for vmlinux**
>>
>>**Solution:** Install dwarves package(**Debugging Information Manipulation Tools:**)
>>
>>dwarves is a set of tools that use the debugging information inserted in ELF binaries by compilers such as GCC, used by well known debuggers such as GDB, and more recent ones such as systemtap. Utilities in the dwarves suite include pahole, that can be used to find alignment holes in structs and classes in languages such as C, C++, but not limited to these. It also extracts other information such as CPU cacheline alignment, helping pack those structures to achieve more cache hits. A diff like tool, codiff can be used to compare the effects changes in source code generate on the resulting binaries. Another tool is pfunct, that can be used to find all sorts of information about functions, inlines, decisions made by the compiler about inlining, etc.)
>>
>>`$sudo apt-get install dwarves`

## Module Programming

### Basic Module Template creation and compilation

#### Practice1:

* create your own basic module template,compile and try to load into kernel(outside kernel source tree)
* Expected results: on successfull insertion, your module name should be visible by `lsmod` command

##### Problems encountered during compilation of Module

> **Problem1**
>
>>**Makefile:632: include/config/auto.conf: No such file or directory**
>>
>>**ERROR: Kernel configuration is invalid.**
>>
>>**make[2]: *** No rule to make target '/home/km/Downloads/hello/hello.o', needed by '__build'.**
>>
>>**Solution:** Go to kernel source tree and once configure the kernel and compile
>>
>>`make menuconfig`
>>
>>`make`

### Module Dependency

#### Practice1: 

* Create two modules(add.c and avg.c), avg.c module uses add symbol in add.c module and compile and try to load avg.c module
* Expected results: 
* * 1. avg loading gives error as avg module depends on add module(unknown symbol "add")
* * 2. first load add module and next avg module gives success 

##### Problems encountered during compilation of Multiple Modules and Installation

> **Problem1**
>
>> **SSL error:02001002:system library:fopen:No such file or directory: ../crypto/bio/bss_file.c:72**
>> 
>> **SSL error:2006D080:BIO routines:BIO_new_file:no such file: ../crypto/bio/bss_file.c:79**
>> 
>> **sign-file: certs/signing_key.pem: No such file or directory**
>>
>>> **Description:**
>>> ###### **Signed kernel module support**
>>> Since Linux kernel version 3.7 onwards, support has been added for signed kernel modules. When enabled, the Linux kernel will only load kernel modules that are digitally signed with the proper key. This allows further hardening of the system by disallowing unsigned kernel modules, or kernel modules signed with the wrong key, to be loaded. Malicious kernel modules are a common method for loading rootkits on a Linux system.
>>>  ###### **Enabling module signature verification**
>>>  Enabling support is a matter of toggling a few settings in the Linux kernel configuration. Unless you want to use your own keypair, this is all that has to be done to enable kernel module support. It must also be noted that a change of file structure occurred in kernel version 4.3.3. So from this version and above the certificates and a sign files used to manually sign modules has moved into: /usr/src/linux/certs/ Also the sign-file perl script is now directly executable in later kernel versions and does not require you to execute the perl command. Adjust the installation and setup methods accordingly to the kernel version that will be used. 
