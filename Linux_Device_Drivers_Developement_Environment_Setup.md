# Linux Device Drivers Development Enviroment Setup(Kernel Configuration,Compilation and installation(Own Built Kernel))

**Two ways to own built kernel:**
* 1. Manual Method
* 2. Automation Method using script

## Manual Method:
### 1. Install Required packages
		$ sudo apt-get install flex bison ncurses-dev libssl-dev 

### 2. Download kernel source code

 * Create GITHUB folder in home directory
 * 		$ mkdir GITHUB
 * 		$ cd GITHUB
 * 		$ git clone https://github.com/torvalds/linux.git

### 3. Kernel Configuration
*		$ cd linux
*		$ du -sh .
*	1.5G
#### Run Configuration command to configure kernel source code
*		$ make menuconfig
*	(by default configuration file of x86 platform is taken as input to menuconfig and generates .config output (/boot/config-`uname -r`))
*	output of kernel configuration is .config file
*	CONFIG_<...>=y/m/notset; y-static;m-module(dynamic)
### 4. Kernel Compilation
####	static compilation
		$ make -j4(static compilation)
*	output is vmlinux(kernel raw image)-virtual memory image
	
		$ du -sh vmlinux(without compression)
*	534MB
####	Dynamic Compilation
		$ make modules(dynamic compilation)
*	output is .ko file for each =m configured source file
	
		$ du -sh .
*	13G
### 5. Kernel installation
####	Dynamic installation
		$ sudo make modules_install (.ko installation)
*	output is /lib/modules/`uname -r`/
####	Static installation
		$ sudo make install
*	output is /boot/vmlinuz-`uname -r`(vmlinuz is compressed linux kernel)-virtual memory linux gZip
*	output is /boot/config-`uname -r`
*	output is /boot/System.map-`uname -r`
*	output is /boot/initrd-`uname -r`
*	output is /boot/abi-`uname -r`
		$ du -sh vmlinuz-`uname -r`
			6.6 M

### 6. Reboot
		$ sudo reboot
		    

## Automation method(Script)
