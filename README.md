# About

This is a FreeRTOS V8.2.3 (2015) port on IA32 PC, which is modified from the [FreeRTOS port on Intel Galileo](http://www.freertos.org/RTOS_Intel_Quark_Galileo_GCC.html).

# Directory Structure

See [FreeRTOS source code directory structure](http://www.freertos.org/a00017.html). This PC port contains only the files from the Galileo port. The directory Demo/IA32_flat_GCC_Galileo_Gen_2 is renamed to Demo/IA32_flat_GCC_PC.

In Demo/IA32_flat_GCC_PC, Support_Files contains the board supporting package, and the remaining directories are FreeRTOS applications.

# Cross Compiler gcc 8.1.0

 * Install Gentoo Linux e.g. from UbuntuLiveDVD https://github.com/pwasiewi/gentools
 * In Gentoo run: 
 ```
 USE="-fortran nossp" crossdev --target i686-unknown-linux-gnueabi --stable  --gcc 8.1.0-r3 --libc 2.26-r7 --kernel 4.16.12 -oO /usr/portage
 ```

# Build Commands

```
git clone https://github.com/pwasiewi/freertos_x86_gcc_pc.git
cd freertos_x86_gcc_pc/Demo/IA32_flat_GCC_PC/Blinky_Demo
make # generate build/Blinky_Demo.elf
cp build/Blinky_Demo.elf iso/root/boot/
cd iso
./mkiso
qemu-system-i386 -cdrom freertos.iso

```

# Boot Loader

Use a bootloader supporting Multiboot Specification to boot Blinky_Demo.elf

For example, if you use GRUB 2 as the bootloader and put Blinky_Demo.elf in /boot, you need a menuentry in grub.cfg:

```
menuentry 'FreeRTOS Blinky Demonstration' {
    multiboot /boot/Blinky_Demo.elf
}
```
