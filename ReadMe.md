# RomWBW

#### Z80/Z180 System Software

Version 2.9.0, 2018-01-26

Wayne Warthen  
[wwarthen@gmail.com](mailto:mailto:wwarthen@gmail.com "mailto:wwarthen@gmail.com")

__Download:__

  - [RomWBW v2.9.0 Distribution Package](https://www.retrobrewcomputers.org/lib/exe/fetch.php?media=software:firmwareos:romwbw:romwbw-2.9.0-package.zip "software:firmwareos:romwbw:romwbw-2.9.0-package.zip (33.8 MB)")
  - [RomWBW Architecture Document](https://www.retrobrewcomputers.org/lib/exe/fetch.php?media=software:firmwareos:romwbw:romwbw_architecture.pdf "software:firmwareos:romwbw:romwbw_architecture.pdf (1 MB)")

__Related pages:__

  - [RomWBW Applications](https://www.retrobrewcomputers.org/doku.php?id=software:firmwareos:romwbw:apps "software:firmwareos:romwbw:apps")
  - [Z-System Notes](https://www.retrobrewcomputers.org/doku.php?id=software:firmwareos:romwbw:zsystem "software:firmwareos:romwbw:zsystem")
  - [Errata](https://www.retrobrewcomputers.org/doku.php?id=software:firmwareos:romwbw:errata "software:firmwareos:romwbw:errata")

## Summary

RomWBW provides a complete software system for all Z80/Z180 CPU-based
systems produced by the RetroBrew Computers Community including the SBC
1/2, Zeta 1/2, N8, Mark IV, and RC2014. Virtually all RetroBrew hardware
is supported including floppy, hard disk (IDE, CF Card, SD Card), Video,
and keyboard. VT-100 terminal emulation is built-in for all video
adapters.

In addition to a simple system monitor, RomWBW includes robust
adaptations of both CP/M-80 2.2 and Z-System (ZCPR + ZSDOS). Either
operating system can be loaded directly from ROM or installed and loaded
from disk storage. A selection of standard/useful applications is
provided via a built-in ROM disk. A RAM disk is also provided for
fast/temporary file storage.

A pre-built ROM image is included for each platform. If desired, system
customization is achieved by making simple modifications to a
configuration file and running a build script to generate a custom ROM
image. All source and build tools are included in the distribution. The
build scripts run under any modern 32 or 64 bit version of Microsoft
Windows.

John Coffman's UNA hardware BIOS is fully supported by RomWBW. See the
section below for more information on running RomWBW on top of UNA.

## Installation

In general, you will just program your system's ROM with the appropriate
ROM image from the RomWBW distribution. This can be done with a ROM
programmer. Alternatively, if your system supports in-situ ROM
programming, you can use Will Sowerbutts' FLASH application which has
been included in recent RomWBW distributions.

The pre-built ROM images will automatically detect and support a
reasonable range of devices including serial ports, video adapters,
on-board disk interfaces, and PropIO/ParPortProp boards without building
a custom ROM.

RomWBW is distributed as a package (zip archive) containing the
pre-built ROM images, source code, and all required build tools. To use
a pre-built ROM image, download the distribution package to a modern
computer (Windows, Mac, Linux, etc.). Unzip the archive using any of the
common zip management applications. You will see that the distribution
is broken up into a few sub-directories. The Binary directory contains
the pre-built ROM images. Based on the table below, pick the appropriate
ROM image:

| Platform       | ROM&nbsp;Image&nbsp;File | Built-in Device Support                                                                                   |
| -------------- | ------------------------ | --------------------------------------------------------------------------------------------------------- |
| SBC&nbsp;V1/V2 | SBC\_std.rom             | Supports onboard PPIDE disk, VGA3/CVDU video/kbd, PropIO (video, kbd, SD Card)                            |
| Zeta&nbsp;V1   | ZETA\_std.rom            | Supports ParPortProp (video, kbd, SD Card)                                                                |
| Zeta&nbsp;V2   | ZETA2\_std.rom           | Supports ParPortProp (video, kbd, SD Card)                                                                |
| N8             | N8\_std.rom              | Supports onboard SD Card, video, keyboard; production board assumed (date code \>= 2312)                  |
| Mark&nbsp;IV   | MK4\_std.rom             | Supports onboard SD Card, IDE Disk, VGA3/CVDU video/kbd, PropIO (video, kbd, SD Card)                     |
| RC2014         | RC\_std.rom              | Requires Scott Baker 512KB RAM/ROM module; supports ACIA, SIO/2, Compact Flash, PPIDE, and Floppy modules |

Your system&nbsp;does **not** need to have all the devices listed above to
use the pre-built ROM. The devices will be detected and used only if
present. All you need to have is the CPU board with ROM/RAM and a serial
port. All pre-built ROM images are simple 512KB binary images. If your
system utilizes a 1MB ROM, you can just program the image into the first
512KB of the ROM. The ReadMe.txt file in the Binary directory has more
detailed information on the pre-built ROM images.

Connect a serial terminal or computer with terminal emulation software
to the primary RS-232 port of your CPU board. A null-modem connection
will generally be required. Set the line characteristics to 38400 baud,
8 data bits, 1 stop bit, no parity, and no flow control. Select VT-100
terminal emulation. RC2014 serial port baud rate is determined by
hardware, but is typically 115200 baud.

Upon power-up, your terminal should display a sign-on banner within 2
seconds followed by hardware inventory and discovery information. When
hardware initialization is completed, a boot loader prompt allows you to
choose a ROM-based operating system, system monitor, or boot from a disk
device.

## Upgrading

Program a new ROM chip from an image in the new distribution. Install
the new ROM chip and boot your system. At the boot loader "Boot:"
prompt, select either CP/M or Z-System to load the corresponding OS
directly from ROM.

If you have spare ROM chips for your system, it is always safest to keep
your existing, working ROM chip and program a new one with the new
firmware. If the new one fails to boot, you can easily return to the
known working ROM.

If you use a customized ROM image, it is recommended that you first try
a pre-built ROM image first and then move on to generating a custom
image.

It is entirely possible to reprogram your system ROM using the FLASH
utility from Will Sowerbutts on your ROM drive (B:). In this case, you
would need to transfer the new ROM image to your system using XModem.
Obviously, there is some risk to this approach since any issues with the
programming or ROM image could result in a non-functional system.

Once you have successfully booted your system with the new ROM, you
should update the system software from previous releases that you may
have copied to disk drives. This is described below.

If your system has any bootable drives, then update the OS image on each
drive using SYSCOPY. For example, if C: is a bootable drive with the
Z-System OS, you would update the OS image on this drive with the
command:

``` code
 B>SYSCOPY C:=B:ZSYS.SYS
```

If you have copies of any of the system utilities on drives other than
the ROM disk drive, you need to copy the latest version of the programs
from the ROM drive (B:) to any drives containing these programs. For
example, if you have a copy of the ASSIGN.COM program on C:, you would
update it from the new ROM using the COPY command:

``` code
 B>COPY B:ASSIGN.COM C:
```

The following programs are maintained with the ROM images and all copies
of these programs should be updated when upgrading to a new ROM version:

  - ASSIGN.COM
  - FORMAT.COM
  - OSLDR.COM
  - SYSCOPY.COM
  - TALK.COM
  - FDU.COM (previously FDTST.COM)
  - XM.COM
  - MODE.COM
  - RTC.COM
    
## Usage Instructions

A typical set of CP/M-80 2.2 and Z-System applications are included on
the ROM file system. The Doc directory of the distribution contains the
CP/M, ZSDOS, and ZCPR user manuals which provide the primary usage
information. Note that the Z-System applications will generally not run
under CP/M.

The following custom applications are included on the ROM disk to
enhance the operation of
RomWBW:

| Appplication | Description                                                                                                                          |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| ASSIGN.COM   | Add, change, and delete drive letter assignments. Use ASSIGN /? for usage instructions.                                              |
| SYSCOPY.COM  | Copy system image to a device to make it bootable. Use SYSCOPY with no parms for usage instructions.                                 |
| FDU.COM      | Format and test floppy disks. Menu driven interface.                                                                                 |
| OSLDR.COM    | Load a new OS on the fly. For example, you can switch to Z-System when running CP/M. Use OSLDR with no parms for usage instructions. |
| FORMAT.COM   | Will someday be a command line tool to format floppy disks. Currently does nothing\!                                                 |
| MODE.COM     | Reconfigures serial ports dynamically.                                                                                               |
| XM.COM       | XModem file transfer program adapted to hardware. Automatically uses primary serial port on system.                                  |
| FLASH.COM    | Will Sowerbutts' in-situ ROM programming utility.                                                                                    |

Please see the [RomWBW Applications](https://www.retrobrewcomputers.org/doku.php?id=software:firmwareos:romwbw:apps "software:firmwareos:romwbw:apps")
page for more information on using these applications.

Check the [Errata](https://www.retrobrewcomputers.org/doku.php?id=software:firmwareos:romwbw:errata "software:firmwareos:romwbw:errata")
page for current usage notes.

## UNA Hardware BIOS

John Coffman has produced a new generation of hardware BIOS called UNA.
The standard RomWBW distribution includes it's own hardware BIOS.
However, RomWBW can alternatively be constructed with UNA as the
hardware BIOS portion of the ROM. If you wish to use the UNA variant of
RomWBW, then just program your ROM with the ROM image called
"UNA\_std.rom" in the Binary directory. This one image is suitable on
**all** of the platforms and hardware UNA supports.

UNA is customized dynamically using a ROM based setup routine and the
setup is persisted in the system NVRAM of the RTC chip. This means that
the single UNA-based ROM image can be used on most of the RetroBrew
platforms and is easily customized. UNA also supports FAT file system
access that can be used for in-situ ROM programming and loading system
images.

While John is likely to enhance UNA over time, there are currently a few
things that UNA does not support:

  - Floppy Drives
  - Terminal Emulation
  - Zeta 1 and N8 Systems
  - Some older support boards
    
The UNA version embedded in RomWBW is the latest production release of
UNA. RomWBW will be updated with John's upcoming UNA release with
support for VGA3 as soon as it reaches production status.

Please refer to the [UNA BIOS Firmware Page](https://www.retrobrewcomputers.org/doku.php?id=software:firmwareos:una:start "software:firmwareos:una:start")
for more information on UNA.

## CP/M vs. Z-System

There are two OS variants included in this distribution and you may
choose which one you prefer to use. Both variants are now included in
the pre-built ROM images. You will be given the choice to boot either
CP/M or Z-System at startup.

The traditional Digital Research (DRI) CP/M OS is the first choice. The
Doc directory contains a manual for CP/M usage ("CPM Manual.pdf"). If
you are new to the RetroBrew Computer systems, I would currently
recommend using the CP/M variant to start with simply because it has
gone through more testing and you are less likely to encounter problems.

The other choice is to use the most popular non-DRI CP/M "clone" which
is generally referred to as Z-System. Z-System is intended to be an
enhanced version of CP/M and should run all CP/M 2.2 applications. It is
optimized for the Z80 CPU (as opposed to 8080 for CP/M) and has some
significant improvements such as date/time stamping of files. For
further information on the RomWBW implementation of Z-System, see the
wiki page [Z-System Notes](https://www.retrobrewcomputers.org/doku.php?id=playground:wwarthen:zsystem "playground:wwarthen:zsystem").
Additionally, the official documentation for Z-System is included in the
RomWBW distribution Doc directory ("ZSDOS Manual.pdf" and "ZCPR Manual.pdf").

## ROM Customization

The pre-built ROM images are configured for the basic capabilities of
each platform. If you add board(s) to your system, you will need to
customize your ROM image to include support for the added board(s).

Essentially, the creation of a custom ROM is accomplished by updating a
small configuration file, then running a script to compile the software
and generate the custom ROM image. At this time, the build process runs
on Windows 32 or 64 bit versions. All tools (compilers, assemblers,
etc.) are included in the distribution, so it is not necessary to setup
a build environment on your computer.

For those who are interested in more than basic system customization,
note that all source code is provided (including the operating systems).

Complete documentation of the customization process is found in the
ReadMe.txt file in the Source directory.

Note that the ROM customization process does not apply to UNA. All UNA
customization is performed within the ROM setup script.

## Source Code Respository

All source code and distributions are maintained on GitHub. Code
contributions are very
welcome.

[https://github.com/wwarthen/RomWBW](https://github.com/wwarthen/RomWBW "https://github.com/wwarthen/RomWBW")

## Distribution Directory Layout

The RomWBW distribution is a compressed zip archive file organized in a
set of directories. Each of these directories has it's own ReadMe.txt
file describing the contents in detail. In summary, these directories
are:

| Directory | Description                                                                                                                             |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Binary    | The final output files of the build process are placed here. Most importantly, are the ROM images with the file names ending in ".rom". |
| Doc       | Contains various detailed documentation including the operating systems, RomWBW architecture, etc.                                      |
| Source    | Contains the source code files used to build the software and ROM images.                                                               |
| Tools     | Contains the MS Windows programs that are used by the build process or that may be useful in setting up your system.                    |

## Acknowledgements

While I have heavily modified much of the code, I want to acknowledge
that much of the work is derived or copied from the work of others in
the RetroBrew Computers Community including Andrew Lynch, Dan Werner,
Max Scane, David Giles, John Coffman, and probably many others I am not
clearly aware of (let me know if I omitted someone\!).

I especially want to credit Douglas Goodall for contributing code, time,
testing, and advice. He created an entire suite of application programs
to enhance the use of RomWBW. However, he is looking for someone to
continue the maintenance of these applications and they have become
unusable due to changes within RomWBW. As of RomWBW 2.6, these
applications are no longer provided.

David Giles has contributed support for the CSIO support in the SD Card
driver.

Ed Brindley has contributed some of the code that supports the RC2014
platform.

UNA BIOS is a product of John Coffman.

## Getting Assistance

The best way to get assistance with RomWBW or any aspect of the
RetroBrew Computers projects is via the community
forum.

[https://www.retrobrewcomputers.org/forum/](https://www.retrobrewcomputers.org/forum/ "https://www.retrobrewcomputers.org/forum/")

Also feel free to email Wayne Warthen at
[wwarthen@gmail.com](mailto:wwarthen@gmail.com "wwarthen@gmail.com").
