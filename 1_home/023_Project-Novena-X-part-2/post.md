Title: Project Novena-X Part 2: SATA, full disk encryption, and physical chassis design
----
Author: Dileep
----
Date: August 08, 2015
----
Tags: all open-hardware open-source linux novena software NSA hacking hacker electronics cryptography security machine laptop DIY
----
Text:


(image: sdcard.jpg width: 600 caption: SD card memory partitions)

So far we have a functioning Debian operating system (a flavor/distribution of Linux) that is booting off of the SD card. The SD card has three partitions, which can be accessed from inside Linux as file descriptors (everything in Linux is a file descriptor). Typically, these partitions are present in the ```/dev``` folder. Open up a terminal on your Novena and execute:

```
> ls /dev/mmblk*
```

to see the partitions. These partitions are all already mounted. You can verify this with:

```
> df -h
```

The ```-h``` flag commands ```df``` to dump the sizes of the mounted partitions in human readable units instead of just bytes. As can be seen in the output (and the figure above), the first partition of the SD card ```/dev/mmblk0p1``` is mounted as ```/boot```, and is indeed the boot partition. The size of this partition is really small (100 MB?) because that is all the space it will ever need. You can list its contents with:

```
> ls /boot
```

You will notice that among other files, there are two sets of two specific files: the device tree ```novena.dbt```, the compressed kernel image file ```zImage```, and their recovery counterparts ```novena.dbt.recovery``` and ```zImage.recovery```. There are several bootloader programs available for loading up operating systems, and we are using U-boot. The ```zImage``` file is a compressed version of the Linux kernel that can be quickly loaded into RAM memory instead of having to read the kernel afresh from the root partition. Everytime we upgrade the Linux kernel on our machine, a new image file for it will be generated and placed in the boot partition. We will get to the recovery files in a bit, as these are specific to Novena, and are not standard.

Apart from the big root partition, we have also deliberately created a 6 GB swap partition. This is not revealed by the ```df``` command, so execute ```> cat /proc/swaps```. The Swap space is meant for Linux to dump rarely-used contents of RAM into when it is running out of space in RAM. This is helpful for computers with low RAM. Our machine has 4 GB of RAM and will not (I hope) be used for anything that is RAM intensive. So the function of swap here is to hold the contents of RAM when the machine is suspended-to-disk, or goes into sleep mode, as laptops tend to do when we close the lid. Since RAM is volatile memory, it needs to be constantly powered for the memory to remain there unaffected (there is a caveat to this that I will be addressing shortly). But the disk (in our case, SD card) is persistent memory. So the contents of RAM can be dumped onto it indefinitely, and recovered error free on demand.


# Basic SATA (unencrypted) installation

We installed (flashed really) an OS image onto our SD card using another computer. But now we shall install a bootstrapped Debian onto a SATA Solid-State disk (SSD) from within Novena booted off of the SD card. This will result in a drastic increase in the speed of the machine, as most of the bottleneck you are experiencing right now is from the read/write speed limits of the SD card. We will first do a clean by-the-book install without encryption just to ensure that everything is working, using instructions from (link: https://novena-guide.readthedocs.org/en/PVT2/ text: https://novena-guide.readthedocs.org/en/PVT2/ popup: yes). For this, we will need to have connected the SATA disk to the Novena board before booting it. If it has been detected by the kernel as a device, it should show up as ```/dev/sda```, or ```/dev/hda``` if it isn't an SSD. There may be additional numbered devices such as ```/dev/sda1```, ```/dev/sda2``` and so forth if the disk already contained partitions. These are irrelevant as we will be erasing them and making our own. We will also need a working internet connection on our Novena. If you have plugged in an ethernet cable, it should just work out of the box. To verify, ping a website like google using ```> ping www.google.com```, and see if any of your ping packets make it through and are returned. You could try and use the browser **iceweasel** for this as well.

The first thing we will do is upgrade all the components of our system, so only the newest programs make it into the SATA installation. To do this, we use the Debian package manager called **Aptitude**. All Linux distributions come with their own package managers and official repositories for software. While we don't HAVE to rely on them to install open source software, they help in resolving dependencies and general bookkeeping. **Aptitude** is very simple to use. For example, to search for a specific program (say **GIMP**) in the configured repositories, just use ```> sudo apt-cache search gimp```. To install it, use ```> sudo apt-get install gimp```. This will install **GIMP**, as well as other programs and libraries that **GIMP** will require, as long as they are available in the repositories that we have configured **Aptitude** to use. To remove **GIMP**, use ```> sudo apt-get remove gimp```. To remove other programs and libraries that were installed automatically with **GIMP** and aren't being used by any other programs that **Aptitude** has installed on your computer, just use ```> sudo apt-get autoremove```.

After our fresh SD card flash, we need **Aptitude** to compile an updated list of available packages and versions from the repositories. For this, execute:

```
> sudo apt-get update
```

After it compiles and updates list, we can get it to upgrade any packages currently installed on our system that are out-of-date, using:

```
> sudo apt-get upgrade
```

Depending on the number of packages on your computer, this may take a while. If by chance your Linux kernel also gets upgraded, then it is best to restart the computer using ```> sudo reboot```. You can verify the version of the kernel that has been currently loaded using ```> uname -a```. Before you restart, if you have a wifi network available, and would rather use that instead of an ethernet cable, then I recommend installing **wicd** and related packages:

```
> sudo apt-get install wireless-tools iw wicd-curses wicd-gtk
```

I would also recommend removing the default wifi program called **network-manager**, as it sometimes conflicts with **wicd** for certain kinds of wifi encryption.

To perform a vanilla Debian installation on a connected SATA disk, there is really nothing for me to add. Just follow the instructions on (link: https://novena-guide.readthedocs.org/en/latest/tasks.html text: https://novena-guide.readthedocs.org/en/latest/tasks.html popup: yes). Since this is only a test run, you can remove all the packages from the list after the ```-l``` flag inside ```sata-install.sh``` file to save some time.

# EEPROM

Note that the instructions on the readthedocs page for a clean SATA install ask you to execute the command:

```
> novena-eeprom -f es8328,pcie,gbit,hdmi,eepromoops,sataroot -w
```

This needs some explanation. EEPROM stands for Electronically Erasable Programmable Read-Only Memory. There is a chip on the Novena motherboard right below the RAM card that is an EEPROM chip (See if you can spot it. Use your google-fu and the chip number). This contains a limited amount of memory whose contents can be read by the motherboard during boot, and whose contents can be manipulated by Xob's ```novena-eeprom``` program. This program, like all others we've been using, is open source, and its source is available at (link: https://github.com/xobs/novena-eeprom text: https://github.com/xobs/novena-eeprom popup: yes). The designers of Novena have included some nifty features in the EEPROM, like setting or unsetting a bit in it to enable/disable the regeneration of a new MAC address during boot. The MAC address is how your computer identifies itself to a wifi or ethernet network. Other features can be explored at (link: http://www.kosagi.com/w/index.php?title=Novena/EEPROM text: http://www.kosagi.com/w/index.php?title=Novena/EEPROM popup: yes). The current EEPROM settings can be viewed by simply executing the command ```> novena-eeprom``` without any arguments. If you do this before executing the EEPROM instruction from the readthedocs page, you will notice that all the settings ```(es8328,pcie,gbit,hdmi,eepromoops)``` except ```sataroot``` are present. If you do this after executing that instructional command, ```sataroot``` will now appear in the list. If this option has been enabled in the EEPROM, then the next time you boot, the motherboard will mount the first partition on the SD card as the boot partition, but mount the third partition on the SATA disk as the root partition (as well as mount the second SATA partition as swap, if that is how it is setup in the root partition). Check this by rebooting now.

# Switching between SD card and SATA installation

Once you have booted into the SATA installation, you will notice an immediate improvement in speed. Verify all the mount points by using the ```> df -h``` command. Verify if the swap partition is being used by using the ```> cat /proc/swaps``` command. If you check the contents of ```/dev```, you will see the other SD card partitions, which haven't been mounted. You can check their contents by mounting them manually at specific locations (refer to ```mount```, and ```umount``` commands for help). If you reboot now, you will once again find yourself in the SATA installation environment, but with a boot partition that is on the SD card. While the installation script should create a "boot-partition" on the SATA disk as well, it is not really being used. There is a way to force the motherboard to look for a boot partition on the SATA device by shorting a jumper on the motherboard, but we will explore this in a later post.

If you want to switch back to the SD card installation, then there are two ways of doing this. One is to remove the ```sataroot``` option from the EEPROM settings by executing:

```
> novena-eeprom -f es8328,pcie,gbit,hdmi,eepromoops -w
```

provided that ```novena-eeprom``` had been installed during the SATA installation. If not, you can fix that using **Aptitude**. Now, if you reboot, you should be back in your SD card environment. Another way to boot into the SD card is to boot into its recovery kernel. To do this, simply press and hold the "user" button right next to the "reset" button on the motherboard during boot for about ten seconds. Then, this should dump you into a recovery kernel on the SD card irregardless of the EEPROM settings. Since it is very likely that we upgraded our kernel in the proper SD card environment before the SATA installation, the recovery kernel will perpetually be of an outdated version, which can be verified by ```> uname -a```. Putting the ```sataroot``` back into the EEPROM settings will cause the board to boot back into the SATA environment. This ability to switch between the three kernel environments is important not only for troubleshooting in case of bad goof-ups, but also because this will come in handy for duress boot.

# Full Disk Encryption on Novena

(image: encryption.jpg width: 400 caption: sourced from adwordsredefined.wordpress.com)

Right now, all the contents of the SD card and the SATA disk are completely unencrypted. Which means that anyone with physical access to your computer can take those devices out and read their contents without facing any hurdles. It is generally common practice to encrypt one's hard disk to protect one's private data. What this usually involves is the use of a standard secure encryption method (such as **LUKS**) that has been tested by (and continues to be tested by) the wider community for security vulnerabilities. It is better to use a method that is widely known but also widely scrutinized, instead of trying to invent one's own. Once we encrypt our hard disk (both root and swap partitions), they will need a key in order to be decrypted and read. When ever these partitions are mounted (such as during boot for regular usage), a key will have to be supplied. Now the key can be a passphrase that you'd have to type in, or a key file that you can supply to the computer from some other location (like a USB stick), or a combination of both. The point is that that disk cannot be read unless all key components of the key are available. Different countries have different laws that their border protection agencies have to follow, which will determine whether or not it would be legal to withold an encryption key passphrase from them. In the United States for example, I believe the passphrase counts as a privacy right, and cannot be demanded of you unless they have knowledge of something specific in the data that they already expect to find during the search. A way to get around this is to use a combination of a passphrase and a keyfile, and just not have the keyfile in your immediate possession during a border crossing. These agencies typically reserve the right to make copies of all your memory devices, or indeed confiscate your computer, with the threat of denying you entry if you disagree. They won't get much from copying a well encrypted drive if they don't have the key, but be prepared to lose your machine, and know your laws before you put them to any test, and accept all the risks of your actions.

With that warning out of the way, lets get started! We will be using the ```LUKS``` plus ```dm-crypt``` method for encrypting our root and swap partitions. We won't be encrypting the boot partition on the SD card, since the board will need to read bootloader and kernel image from somewhere before it gets any information about whether or not anything is encrypted, and what to do about it. There may be a way to partially get around this using other bootloaders, but I couldn't find any method for U-boot. One of the great things about open source communities is that almost always, someone will have already solved the problem, or implemented an idea that you have just come up with. In this case, **kosagi** forum members **Rian** and **Jogi** have already done all the hardwork for us. Their efforts, as well as some discussion around the topic can be found at (link: http://www.kosagi.com/forums/viewtopic.php?id=95 text: http://www.kosagi.com/forums/viewtopic.php?id=95 popup: yes). The both of them have uploaded their scripts (which are modifications of the openly available original SATA installation scripts) on their github pages. We will in fact be using **Jogi**'s script for this. He had to downgrade his kernel when he was trying this out in April 2015, but I didn't have to. So my version numbers are newer than his, but the rest of the commands are identical.

To do this, we will need to have booted into the SD card (non-recovery) environment. We can't do this from the recovery environment because the recovery kernel will not match the actual kernel of the regular installation, which prevents us from using the ```dm_mod``` module (I suspect this is what **Jogi** ran into). So, the commands to execute in order are as follows:

```
> sudo apt-get install debootstrap cryptsetup apt-cacher-ng u-boot-tools
> git clone https://github.com/jogi91/novena-image.git
> cd novena-image
> apt-get download u-boot-novena irqbalance-imx novena-eeprom kosagi-repo novena-firstrun
```

The ```git clone``` command creates a folder named ```novena-image```, with **Jogi**'s modified scripts in it. If there already exists a folder with that name (like the original vanilla installation scripts) at your current location, you should rename the old folder to something else. Note that we used **Aptitude** to download ```*.deb``` package files into our current location without installing them. Now, you must use the ```ls``` command to note the version numbers of the ```*.deb``` files that were just downloded from the repositories, and change the contents of the ```encrypted-sata-install.sh``` file to match those. You might also want to add the ```-m http://127.0.0.1:3142/http.debian.net/debian \``` line just the way you did with the vanilla install script. **Jogi** has modified the list of packages after the ```-l``` flag to suit his needs. You are welcome to change them to whatever you like. Now, don't forget to get the kosagi key to setup their repository:

```
> gpg --keyserver keyserver.ubuntu.com --recv-keys 03C7B7EC
>gpg --export 03C7B7EC > kosagi.key
```
With that done, now we can perform an encrypted Debian installation onto the SATA device with the command:

```
> sudo ./encrypted-sata-install /dev/sda
```

The script will prompt you for a passphrase to use as the encryption key for the root partition (Choose well. (link: https://www.youtube.com/watch?v=foil0hzl4Pg#t=14m42s text: Here's some good advice on it popup: yes)). It will in fact ask for this thrice. If the installation goofs up, reboot back into the SD card regular environs and try again, as the partition tables on the SATA disk gets modified by the script. Also remove the ```uEnv.txt``` file that gets created in ```/boot``` everytime you run this again, as the script skips writing it if the file already exists. After this script executes without any errors, the first thing to do is to open the ```uEnv.txt``` file inside ```/boot``` as root with write permissions. There will be a ```\0``` or ```^@``` character in it that will need to be converted into a newline character. After this, modify EEPROM settings to boot into the SATA root partition, hit reboot, and cross your fingers. If it worked, then Novena should ask for your encryption key during boot. Once inside, try executing ```> df -h```. You will see that the encrypted device volumes ```/dev/sda*``` have not been mounted directly, but have instead been mapped to **LUKS** devices inside ```/dev/mapper```. Read the contents of ```/etc/fstab``` and ```/etc/crypttab``` to see how root and swap partitions are really being handled.


# Cold-boot attack, and a problem with encrypted Swap

Encryption works by requiring a decryption key. Once supplied, this key is stored by the computer inside RAM during regular operation, and is used to read/write data from/to the encrypted device. The key ideally disappears from RAM once the computer is powered down. But there is research to suggest that the contents of RAM might not be as volatile as one would hope, and that the data in it can be retrieved from it seconds, and sometimes minutes after the RAM chip has been forcibly yanked out of your running (or just turned off) computer. And if the temperature of the chip is lowered using compressed air cans or dry ice or liquid nitrogen, then the memory will stay persistent for even longer. This is known as the (link: https://en.wikipedia.org/wiki/Cold_boot_attack text: Cold-boot attack popup: yes), and has successfully been demonstrated as a method that can retrieve disk encryption keys from computers that are currently in operation. People generally hotglue their RAM chips to their motherboards, and use tamper-proof screws to delay anyone getting into their box once its been turned off. Just be sure to turn the damn thing off when under attack.

You will realize that although the root partition requires a passphrase key from the user, the swap partition is recreated and encrypted anew with a randomly generated key at every boot. You can look for the line ```cryptsetup -d /dev/urandom create crypt-swap ${swap_part}``` inside the script file ```novena-image.sh``` from **Jogi**'s git project (which should now be inside an unencrypted SD card partition. Do you remember how to mount that?!). This method does not allow you to use the suspend-to-disk functionality, since all the contents of RAM will be stored in the encrypted swap, and will be overwritten as the encrypted swap is recreated when the computer wakes up from suspend state. One way to get around this is to derive the swap key from the root partition decryption key, as suggested on (link: http://madduck.net/docs/cryptdisk/ text: http://madduck.net/docs/cryptdisk/ popup: yes). I haven't tried this yet, but will let you know if it works in a future post.

A word of caution about full disk encryption. Not only will it affect the speed of the machine (since continuous encryption and decryption can be computationally taxing), but the encrypted data will be forever irretrievable if the keys are lost. Rely on backups, but encrypt the backups as well!


# Chassis design update

(image: chassis_plan.jpg width: 800 caption: Chassis design)

Had I infinite time to do this, then I would very likely try to start with a thick aluminium block and mill out sockets for every single component to fit neatly into. However, as a quick and dirty option, I will be screwing flat plates onto 80/20 extruder rods. The overall dimensions will be around 2.25" x 8" x 14", plus hinge thickness and handle thickness. The dimensions aren't metric because I am working in an American machine shop, and will not be exact because I will most definitely make errors while using the shear. But in any case, I wanted 1/16" thick top and bottom plates to screw standoffs into for the board and the LCD. I needed 1/8" front and back plates to screw handles, and screw into the tapped extruder rod centers. The extruder rods need to be of length 7.75" so the plates sit flush with the top and bottom edges. The extruder rod ridges on the interior will be exposed, allowing me to implement a variable angle screen holder using slotted moving hinges, as well as screw other miscellaneous things into (lid closing and locking mechanism, briefcase handles, rack mounts, coffee cup holder, etc.). Progress should be simple and quick, and shouldn't require more than one half-a-day a week. All materials for this were purchased from McMaster Carr.

(image: metal.jpg width: 800 caption: Machine shop antics)

Next post will be about resolving the swap encryption deal, running ther LCD display off of the board's native LVDS port instead of using a HDMI to LVDS driver board, and some more updates on the physical chassis. Stay tuned.
