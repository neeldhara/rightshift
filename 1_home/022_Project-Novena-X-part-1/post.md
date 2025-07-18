Title: Project Novena-X Part 1: Motherboard and basic setup
----
Author: Dileep
----
Date: July 18, 2015
----
Tags: all open-hardware open-source linux novena software NSA hacking hacker electronics cryptography security machine laptop DIY
----
Text:


(image: novena_pvt2_top_sm.jpg width: 1000 caption: sourced from kosagi.com)

The first step is always the hardest. It generally helps for any project to lay out central goals in writing before beginning. Since I intend to actually use the laptop I am building for everyday and special purposes, security figures quite high on that list. And since I've ordered a piece of hardware (the motherboard) from an external source, and the mail package changed several hands in transit, the first fear I have is of hardware modification by mail interception.

# Visual Inspection of the motherboard

Novena is an (link: http://opensource.com/resources/what-open-hardware text: open hardware popup: yes) project. Meaning the mechanical drawings, schematics, the printed-circuit board layout data, the hardware-description language source code and the integrated circuit layout data for the board have been made (link: http://kosagi.com/w/index.php?title=Novena_PVT_Design_Source text: available popup: yes) for the general public to study, modify, create, and redistribute. So if I were thourough, I'd bring out my trusty multimeter, and verify every exposed copper pad and trace on the physical board to check if it matches the design document version. And if I were really paranoid, I'd use the design files to print my own PCB (or use a PCB printing service, such as OSHPark), and buy my own components from various vendors, and solder the board together by myself (In fact, I may still have to do this with the battery board, unless Bunnie decides to start selling off surplus stock on (link: https://www.crowdsupply.com/sutajio-kosagi/novena text: crowdsupply popup: yes) while the summer lasts). Until then, I'll need to physically pull the DC plug from the jack everytime I shut the machine down.

(image: senoko_dvt1_sm.jpg class: floated width: 800 caption: Battery board, sourced from kosagi.com)

But for the poor man's visual inspection, all we really need to look for is a hardware add-on that is obvious to spot with the naked eye. For this, we can rely on the high resolution photographs of the board provided for us at (link: http://www.kosagi.com/w/index.php?title=Novena_PVT_Hardware_Photos text: http://www.kosagi.com/w/index.php?title=Novena_PVT_Hardware_Photos popup: yes). Right off the bat, we encounter a potential problem. The website link begins with a regular ```http```, instead of ```https```. Meaning that there is no telling whether or not an anonymous third party is impersonating ```www.kosagi.com```, and giving me false photographs of the board to work with. SSL style security is a topic worthy of being tackled all by itself (and I intend to do that on this blog eventually), but I'll try and give a brief account of what it means to us later within this post.

The visual inspection process forces one to look the datasheets up for various electronic components, as well as identify the pinouts for all the headers using the (link: http://bunniefoo.com/novena/pvt2_release/SCH-novena_pvt2.PDF text: board schematics popup: yes) file. This exercise is very fruitful, as it reveals all the features and influences future plans about the project. To illustrate, consider the surface-mounted pushbotton labeled "user". If this button is held pushed for ten seconds during boot, Novena boots into a backup kernel from the SD card. This feature will come in handy for a duress boot, where a specific ritual sequence of button presses would be required for a proper boot, and a regular push of a "power" button on the front panel could secretly be triggering a backup boot instead. Next check out the jumpers labelled P_SATA, P_USB, and P_EXT. The boot select header precedence is said to be USB > SATA > EXT. If these jumpers are not closed, then we can deny boot access to specific devices. Next observe the 54-pin FPC connector. This not only has connections for the LCD (which we will be using) but also has pins for a touchscreen or touchpad (pins 1 to 4). The 30-pin, so called "Front panel header" on the back of the board has two USB connections, as well as a KEY_COL3 pin, which can be used to detech whether or not the computer case has been opened (if we hook it up right).

(image: composite01.png class: floated width: 1200 caption: Things to note on the board)

The most interesting features are the P_FUSE pin and the P_TAMPER terminals on the front of the board. A cursory glance at the (link: http://bunniefoo.com/novena/IMX6DQ6SDLSRM_security.pdf text: Freescale chip security datasheet popup: yes) reveals that P_FUSE disables tamper detect if zero. I wonder if this can be used to flush the drive encryption passwords from RAM as and when the case is opened to prevent a cold boot attack. Or to prevent the machine from booting while the case is open. Also note that the board typically comes with a 4GB SD card with pre-installed software. We are of course goind to discard the card and use our own larger one (who knows what has been done to the contents of the card before it reached us!).

# Towards first boot

I will be using another linux machine to prepare and install a bootloader and a debian linux image onto a fresh SD card. The instructions for other OSes will vary. For starters, we'll need to get hold of the latest disk images from the novena repositories, linked to on (link: http://www.kosagi.com/w/index.php?title=Novena_Main_Page text: http://www.kosagi.com/w/index.php?title=Novena_Main_Page popup: yes). Once again, we run into trouble because of the lack of ```https``` in the website address. This warrants an explanation.

When we update our browser installations, we can catch the phrase "ca-certificates" in the ```STDOUT``` info dump that our package manager spits out. These are cryptographically signed digital certificates from a (link: https://en.wikipedia.org/wiki/Certificate_authority text: certification authority, or CA popup: yes). CAs are a third party (typically a company) that can be trusted to verify a server (kosagi) administrator's (Bunnie or Xobs) identity before issuing them a signed certificate. This can be used by the server to authenticate itself with a typical user who is trying to connect to it via a https link. The authentication works by using asymmetric key cryptography (or public-key cryptography), which is a facinating subject in itself. While I do intend to make a post or two on it eventually, for now, I'd recommend checking out (link: https://futureboy.us/pgp.html text: Alan Eliasen's popup: yes) take on it.

Anyway, assuming that we aren't the target of a man-in-the-middle attack, we can get a copy of the disk image by opening up a terminal console and executing the command:

```
> wget http://repo.novena.io/novena/images/novena-mmc-disk-r1.img
```


The kosagi page also provides us with three other pieces of information: an RSA signature, a SHA256 hash, and an MD5 hash. Copy the RSA signature bit into a file named ```novena-mmc-disk-r1.img.asc```. Then run the following command (install gpg if you haven't):

```
> gpg novena-mmc-disk-r1.img.asc
```


We get output:

```
gpg: assuming signed data in 'novena-mmc-disk-r1.img'
gpg: Signature made Sun Dec 21 32:35:33 2014 PST using RSA key ID 6BD61ADA
gpg: Can't check signature: No public key
```


This is because although we have a signature of the disk image made with someone's private key, we don't have their public key (which is required to verify who this is). But the signature includes a key ID ```6BD61ADA``` (which are basically the last few bits of their public key (in hex)). This can be used to search for the public key from one of several public servers, such as ```pgpkeys.mit.edu```. Run:

```
> gpg --keyserver pgpkeys.mit.edu --recv-key 6BD61ADA
```


We get output:

```
gpg: key 6BD61ADA: public key "Sean Cross (Personal address) <sean@xobs.io>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```


It would appear that there is one public key in the record with that ID, and it is associated with a person/entity named Sean Cross. A search on twitter, github, and google (leads to his personal blog) seems to indicate that this might be Sean "Xobs" Cross. But since I have never personally met him to get hold of his public key ID, and don't know anyone who knows someone who has signed his public key (and we don't have a trusted third party CA to rely on), I have no way of knowing if this is Xobs's signature (if you are reading this Xobs, you might want to switch the kosagi link to https :).

For completeness, to verify if the RSA signature came from a private key that is associated with this particular Sean's public key, run gpg signature check again. We get output:

```
gpg: assuming signed data in 'novena-mmc-disk-r1.img'
gpg: Signature made Sun Dec 21 32:35:33 2014 PST using RSA key ID 6BD61ADA
gpg: Good signature from "Sean Cross (Personal address) <Sean@xobs.io>" [unknown]
gpg: 	    	      aka "Sean Cross (Email) <xobs@kosagi.com> [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg: 		There is no indication that the signature belongs to the owner.
Primary key fingerprint: 80BE C21D 6D88 3F58 B3A6 B406 ABB0 15C5 6BD6 1ADA
```


Note that the last few bits of the finger print are identical to the key ID. Now we can check the SHA256 hash. A hash is a fixed length condensed output generated by a deterministic function that can take an input of any size. The SHA256 hash that we have is meant to be a condensed hash of the disk image file. Any change in the disk image file would result in a hash mismatch. This is used not so much for security, but to ensure that large files have transferred over a network without suffering corruption/errors. To check the SHA256 hash, run:

```
> sha256sum novena-mmc-disk-r1.img
```


We get output:

```
26d368cb4b3aa43e411703f8c659d3e229deacfe75af38c1f82489dd9af80dbb  novena-mmc-disk-r1.img
```


which matches the hash on the website. To check the MD5 hash, run:

```
> md5sum novena-mc-disk-r1.img
```


We get output:

```
6923a145cbdc75b420408fc2d09ba4f8  novena-mmc-disk-r1.img
```


Same deal. Although, it is generally advised to not rely on MD5 hashes, as they are prone to hash collisions (where two completely different files can produce the same hash).

Now that we have the image, we can burn it onto an SD card. Insert the SD card into a slot on your computer. It should show up as a new device in the ```/dev/``` location (list all devices in that folder before and after inserting the SD card to check for changes). Then optionally, use ```fdisk``` to remove all existing partitions on the card. Then, run (warning, this will make all previous data on the SD card effectively disappear):

```
> sudo dd if=novena-mmc-disk-r1.img of=<path-to-SD-card-device>
```


What the ```dd``` command did is basically to write all the bits from the image file onto the raw SD card. This includes data about partitions, as well as bootsector data, which always goes in the beginning of any device, outside of any partitions. Now run:

```
> sudo fdisk <path-to-SD-card-device>
```


You should see three partitions listed. Delete old third partition and create new third partition with defaults ('p', 'd', 'n','w'). Then run:

```
> sudo fsck <path-to-SD-card-third-partition>
> sudo resize2fs <path-to-SD-card-third-partition>
```


The previous steps extended the third partition to fill all space in the rest of the SD card (the original image assumes that the SD card has only 4GB in total). If we want the Novena to be able to suspend successfully (and why wouldn't we, since we are building a laptop), we need to extend the swap partition. The swap partition is the region on the hard-disk/SD-card where linux will dump all the contents of the RAM into when it needs to go to sleep. The contents will be read from swap and put back into RAM when it is awoken again. To increase swap size, run:

```
> sudo fdisk <path-to-SD-card-device>
```


Delete old third partition again and create new one with reduced size (by 6G).  Then run fdisk again and delete the old second partition (swap), and recreate it after the last sector of the third partition, and change type to Linux swap (0x82). Then resize2fs the third partition again. After that, we need to put swap headers into the swap partition with the command:

```
> sudo mkswap <path-to-SD-card-second-partition>
```

We are almost done. Now we can plug the SD card into the appropriate slot in the center of the Novena motherboard. When the factory image is first booted, it takes us into a custom written setup environment. We can view this without connecting another monitor to the board and by simply using our regular computer. All we need is a USB-to-TTL FTDI beakout board, which we can plug into the UART connectors on the Novena as shown in the image below:

(image: ftdi.jpg class: floated width: 600 caption: FTDI connection to the Novena gives us a console)

After connecting FTDI cable, run:

```
> screen <path-to-ftdi-tty-device> 115200
```


and follow the instructions after powering the board up. I have had bad experiences with using the ```screen``` utility for this, as some of the text came out garbled. It might be better to use another monitor with a HDMI connection and a USB keyboard connected to the Novena board itself. If you managed all this without any hitches, you should be seeing something like this:

(image: setup_sofar.jpg width: 800 caption: first w00t)

Most of these instructions can be found at (link: https://novena-guide.readthedocs.org/en/PVT2/ text: https://novena-guide.readthedocs.org/en/PVT2/ popup: yes), which oddly enough is a ```https``` link (yay). So refer to it if you run into trouble. In the next post, I'll be throwing in an SSD, dealing with full-disk encryption, and updating you on the case design front.



