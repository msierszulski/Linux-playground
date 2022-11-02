# Lab 4 - Buildroot
The purpose of the lab is to learn about the Buildroot tool and its features.

By doing the lab, the user will learn to:
 - Build your own operating system based on the Linux kernel.
 - Configure the tool to customize the operating system.
 - Add custom applications to the operating system.
 - Create patches for off-the-shelf software.

Tasks:
 - Add the chocolate-doom game to the project.
 - Add your own program to the BuildRoot package, e.g. hello_world.
 - Create a patch with your changes.

Platform: `vexpress_ca9x4`

## Solution

1. Download and build Buildroot:

    ```bash
    git clone git://git.buildroot.net/buildroot
    cd buildroot
    make qemu_arm_vexpress_defconfig
    ```
2. Apply patch:

    ```bash
    git apply ../labs/lab4/lab4-ans.patch
    ```

3. Run menuconfig:

    ```bash
    make menuconfig
    ```

4. Add option to build chocolate-doom `target packages -> games -> chocolate doom`.

5. Add option to build Hello world package `target packages -> misc -> Hello World`.

6. Build buildroot:

    ```bash
    make -j6
    ```

7. Run qemu:

    ```bash
    qemu-system-arm -M vexpress-a9 -smp 1 -m 256 -kernel output/images/zImage -dtb output/images/vexpress-v2p-ca9.dtb -drive file=output/images/rootfs.ext2,if=sd,format=raw -append "console=ttyAMA0,115200 rootwait root=/dev/mmcblk0" -serial stdio -net nic,model=lan9118 -net user
    ```
