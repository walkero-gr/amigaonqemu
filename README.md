# amigaonqemu
Here you will find some Makefile scripts and information on how to run AmigaOS 4 and MorphOS on Qemu. This script should work fine on Windows, MacOS X and Linux. It is tested only on Linux Manjaro though.

## Prerequisites
To use this makefile scripts you will need:
* The qemu-ppc v6 and above installed and configured on your system
* To run AmigaOS 4 you will need an ISO of the latest AmigaOS 4.1 Final Edition for Sam460 machine
* To run MorphOS you will need the latest available ISO from https://morphos-team.net/downloads
* `make` command to work on your machine

## How to use
### Create a hard disk
To create a hard disk for your emulated machine you have to do the following.

1. Open the terminal and go inside the **AmigaOS4** or **MorphOS** folder
2. run one of the following commands, depending what you wanna do:
   * `make newhd` to create a 255MB hard disk file with name **newdisk.qcow2**
   * `make newhd HDSIZE=512M` to create a 512MB hard disk file with name **newdisk.qcow2**
   * `make newhd HDSIZE=512M HDNAME=anyname` to create a 512MB hard disk file with name **anyname.qcow2**

**WARNING: If the hard disk image file already exists, it will be overwritten without warning.**

## Run AmigaOS 4
To run AmigaOS 4 follow the next steps:

1. Copy **Sam460InstallCD-53.58.iso** in the **AmigaOS4** folder. That is the default ISO filename the script uses. If your filename is different, either rename it or you can set it with the argument `CD`
2. Make sure you created a hard disk file with `make newhd`. More options can be seen above.
3. Open the terminal and go inside the **AmigaOS4** folder
4. Run `make bootcd` to start the installation
5. After you do the installation, close the emulator and run it with empty cd rom with `make CD=` to boot with your hard disk image. If you want to boot and have a CD-Rom already mounted, you can do it with `make CD=cdrom-image.iso`.

### Setup audio under AmigaOS 4
To setup audio, open the AHI Prefs and set all the sound units to **SB128: HiFi 16 bit stereo++**. 

If it sounds a little bit broken when you play a test sound, would propose to 8 channels, Freq. 44100 Hz and the **Default anti-click time** at the **Advanced** tab to 5ms

### Setup network under AmigaOS 4
To setup network, open the Internet > New Connection app and set the following on every step:

1. Select **Local Area Network** and click **Next** button
2. Select **Manual configuration** and click **Next** button
3. Select **Realtek RTL 8139** from the list and click **Next** button
4. In **Gateway** and **Domain name server** fields insert `10.0.2.2` and click **Next** button
5. Click **Finish** button

### Insert or change a CD-Rom
If you need to insert or change a CD-Rom while the emulator is running, you have to open the **compatmonitor0** view (CTRL+ALT+2 on Linux) from the menu and run the following:

- To eject the currently inserted CD-Rom, type `eject -f cd` and press Enter
- To insert a CD-Rom, type `change cd <path to the iso file>`, i.e `change cd ./Sam460InstallCD-53.58.iso`, and press Enter

Then you have to change again the view to sm501 (CTRL+ALT+1 on Linux) so to go back to AmigaOS 4.

## Run MorphOS 3
To run MorphOS 3 follow the next steps:

WIP