# Lab 1 - u-boot
The purpose of the lab is to familiarize the user with the u-boot startup program and its basic properties.

By doing the lab, the user will learn to:
 - Build a u-boot startup program.
 - Run custom applications in the u-boot environment.
 - Automate the system boot process.

Tasks:
 - Run the hello_world.bin program, located in examples/standalone, using the tftp command in the u-boot console.
 - Modify the u-boot source files so that u-boot automatically loads the hello_world.bin program.
 - Explain the significance of the various options of the qemu-system-arm program that were used in this lab.

Platform: `vexpress_ca9x4`

## Solution

1. Download u-boot:

    ```bash
    git clone git://git.denx.de/u-boot.git
    cd u-boot
    git checkout v2019.04
    ```

2. Apply solution of tasks:

    ```bash
    git apply ../labs/lab1/lab1-ans.patch
    ```

3. Configuring and building u-boot

    ```bash
    make vexpress_ca9x4_defconfig ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-
    make -j4 ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-
    ```

4. Create /home/student/tftp dir

    ```bash
    mkdir -p /home/student/tftp
    ```

5. Copy `hello_world.bin` to tftp folder:
   ```bash
   cp examples/standalone/hello_world.bin /home/student/tftp
   ```

6. Run qemu:

    ```bash
    QEMU_AUDIO_DRV=none qemu-system-arm -M vexpress-a9 -m 256M -serial stdio -monitor none -nographic -kernel u-boot -net nic -net user,tftp=/home/student/tftp
    ```

## Output
After boot sequence you should see:
```bash
...
## Starting application at 0x60008000 ...
Example expects ABI version 9
Actual u-boot ABI version 9
Hello World
argc = 1
argv[0] = "0x60008000"
argv[1] = "<NULL>"
Hit any key to exit ...
```

