# Turning a Regular USB Flash Drive into a USB Rubber Ducky
![[Pasted image 20221031100943.png]]
# Prerequisites

A USB is a really universal interface. Just think how many devices we connect it to and how many devices it works with! Mouses, keyboards, printers, scanners, gamepads, modems, access points, web cameras, telephones, etc. Without thinking, we plug the USB into the socket and the OS automatically determines the type of device and loads the required drivers.

But how does it do it?

# How flash drives work

In fact, the OS knows nothing about the connected device. It has to wait until the device tells it what kind it is. Let's consider a simple example. When we plug a USB flash drive into a USB socket, the flash drive informs the operating system of its type and volume. It is worth remembering our shrewd Chinese colleagues, who learned how to produce higher capacity flash drives (some almost 2 TB). To figure out how this is possible, let's remember (or learn) how the OS recognizes USB devices.

![[Pasted image 20221031101043.png]]

A USB flash drive without its pretty case

# USB device initialization algorithm

The purpose of USB devices is defined by class codes communicated to the USB host for installation of the necessary drivers. The class codes allow the host to work with single-type devices from different manufacturers. The device may support one or several classes, the number of which is determined by the number of USB endpoints. When connected, the host requests a range of standard details from the devices (descriptors), which it uses to decide on how to work with it. The descriptors contain information about the manufacturer and device type, which the host uses to select the program driver.

A regular USB flash drive will have class code 08h (Mass Storage Device — MSD), while a web camera equipped with a microphone will have two codes: 01h (Audio) and 0Eh (Video Device Class).

![[Pasted image 20221031101113.png]]

Device classes

When connected, the USB device is registered, receives an address and sends its descriptor/descriptors to allow the OS to install the necessary drivers and send back the required configuration. After that, the host immediately starts working with the device. Once the work is completed, the device is de-registered. It is important to note that the devices may have several descriptors, they can also de-register and register as a different device.

If you open the body of a USB flash drive, in addition to the mass storage visible to the user, there is a controller responsible for the above-described actions.

![[Pasted image 20221031101139.png]]

# Bad USB or some history

At the last year's Black Hat conference, two researchers (Karsten Nohl and Jakob Lell) shared their experience on how to install a personal upgrade to the firmware of the USB flash drive controller. After a while, this USB flash drive was registered as a keyboard and entered the selected commands. Due to the serious nature of the problem, the guys decided not to make the code for this available. However, soon after, two other researchers (Adam Caudill and Brandon Wilson) presented to the whole world at Derbycon conference an operable PoC tailored to Phison 2251-03 microcontroller [The code is available at GitHub](http://goo.gl/pxYYVQ).

# Transformation

As you might have guessed, today we will try to turn a regular USB flash drive into a pentester's secret weapon!

First of all, we will need a suitable device. As the code has been uploaded for the specific microcontroller only, we have two options — either find a USB flash drive managed by this controller, or perform some very challenging work researching and upgrading the firmware of another microcontroller. This time, we will select an easier way and try to find a suitable USB flash drive (here is [the list of vulnerable equipment](http://goo.gl/MmBgf6)). The controller is quite popular, so, miraculously, I found a suitable USB flash drive among the dozen I have at home.

# Starting the magic

Having found the suitable device (which we won't miss if it fails), we can start its transformation. First of all, we need to download the sources which the guys made available. Actually, the content is described in detail on their official wiki page, but, just in case, I will remind you what they have uploaded to GitHub:

-   DriveCom — an app for communicating with Phison USB flash drives;
-   EmbedPayload — an app for embedding Rubber Ducky inject.bin key scripts into custom firmware for subsequent execution when the USB flash drive is connected;
-   Injector — an app that extracts addresses from the firmware and embeds the patching code in the firmware;
-   firmware — custom 8051 firmware written in C;
-   patch — collection of 8051 patches written in C.

# Preparing the system

Having downloaded the archive with sources from GitHub, you will find that most of them have been written in C# and require compilation, so you will need a studio. Another tool you will need is the [Small Device C Compiler](http://goo.gl/UoIwgd), or SDCC. Install it in `C:\Program Files\SDCC`, you will need it to compile firmware and patches.

Having compiled all the tools contained in the archive, check again if this USB flash drive is suitable for firmware upgrade:

```
DriveCom.exe /drive=F /action=GetInfo
```

where `F` is the letter of the drive.

# Getting the burner image

The next important step is to select an appropriate burner image (8051 binary file, responsible for dumping activities and uploading firmware to the device). They are typically named:

```
BNxxVyyyz.BIN
```

where `xx` is the controller version (for instance, for PS2251-03 it will be 03), `yyy` is version number (not important), and `z` reflects the memory page size and can look like:

-   2KM — for 2K NAND chips;
-   4KM — for 4K NAND chips;
-   M — for 8K NAND chips.

You can look for a suitable burner image for your USB flash drive [here](http://goo.gl/XdrUIm).

# Dumping the original firmware

Before commencing your dirty experiments which could kill the USB flash drive, it is strongly recommended to dump the original firmware, so that if something goes wrong you can try to recover the device. First, switch the device to boot mode:

```
tools\DriveCom.exe /drive=F /action=SetBootMode
```

Then, use the DriveCom utility, passing the drive letter, the path to the burner image, and the path to the file where the original dumped firmware will be saved. It will look like this:

```
tools\DriveCom.exe /drive=F /action=DumpFirmware /burner=BN03V104M.BIN /firmware=fw.bin
```

If you have done everything correctly, the source firmware will be saved to the `fw.bin` file.

# Preparing the payload

Now it's time to think about the functions we want our USB flash drive to have. Teensy has a separate Kautilya toolkit, which can be used to automatically create payloads. For USB Rubber Ducky, there is a whole [website](http://goo.gl/b6OdJv), with a friendly interface, which lets you create any scripts for your device online. This is in addition to the list of finished scripts, which [are available on the project's GitHub](http://goo.gl/O9JGqX). Fortunately, Ducky scripts may be converted into binary to embed them then into firmware. To do this, we will need a utility [Duck Encoder](http://goo.gl/9FNku3).

As for the scripts, there are several options:

-   you can write the required script yourself, as the used syntax is easy to master (see the project's official website);
-   use finished ones uploaded to GitHub. As they have a reverse shell and other goodies — you will only have to make minor corrections and convert them into binary form;
-   or use the above-mentioned website, which will lead you step-by-step through all the settings and will let you download the finished script in the form of a Ducky script (or already in converted binary form).

To convert the script into binary, execute the following command:

```
java -jar duckencoder.java -i keys.txt -o inject.bin
```

where `keys.txt` is a Ducky script, and `inject.bin` is the source binary file.

# Flashing the firmware

As soon as we have the finished payload, it's time to embed it into the firmware. This is done with the following two commands:

```
copy CFW.bin hid.bin
tools\EmbedPayload.exe inject.bin hid.bin
```

Please note that the firmware is first copied to `hid.bin`, and only then is it flashed. This is because the payload can only be embedded into the firmware once, so the original `CFW.bin` must be left untouched.

After this manipulation, we will have a `hid.bin` custom firmware file with an embedded payload. You will only have to place the obtained firmware in the flash drive:

```
tools\DriveCom.exe /drive=F /action=SendFirmware /burner=BN03V104M.BIN /firmware=hid.bin
```

where `F` is the drive letter.

# Alternative options

In addition to using the HID nature of the USB flash drive and turning it into a keyboard which types our payloads, there are some other tricks that can be done. For instance, you can create a hidden partition on the device, decreasing the space seen by the OS. To do this, you will first need to determine the number of logical blocks on the device:

```
tools\DriveCom.exe /drive=E /action=GetNumLBAs
```

Then find the `base.c` file in the `patch` folder, uncomment the line `#define FEATURE_EXPOSE_HIDDEN_PARTITION` and add another directive — `define`, which sets a new LBA number: `#define NUM_LBAS 0xE6C980UL` (this number must be even, so if you got, say, `0xE6C981` at the previous step, you can decrease the number to `0xE6C940`, for example).

Having edited the sources, you need to place the firmware which you want to patch into the `patch` folder, name it `fw.bin` and run `build.bat`, which will create a modified `fw.bin` file in `patch\bin\`. You can now flash this to the USB flash drive.

The options Password Patch and No Boot Mode Patch are done in the same way; you can read more about them on the project's GitHub. My primary goal was to teach the USB flash drive to perform pre-set actions, which we have accomplished.

# Result

We have reached our goal. Moreover, I hope you now understand that USB flash drives (and other USB devices) can no longer be seen simply as a drive that stores your information. In fact, it is almost a computer, which can be taught to execute specific tasks. Although, PoC has so far only been made available for a specific controller, you can be sure that, as you are reading this article, someone is definitely working on others.

So, be careful when you plug in a USB device and keep your eyes open.


## HINT

If the experiments have gone wrong and the USB flash drive behaves in a weird way, you can try to bring it back to life by manually switching it into boot mode and using the utility to restore the original firmware. To do this, before you connect it, you need to close contacts 1 and 2 (sometimes 2 and 3) of the controller, which are located diagonally from the point (see image). Then you can try to bring the device back to life by using the official utility [MPAL](http://goo.gl/J3Jvz0)
![[Pasted image 20221031101249.png]]
Switching a USB flash drive into boot mode by closing the shown contacts

---