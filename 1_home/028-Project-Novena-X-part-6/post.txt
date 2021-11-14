Title: Project Novena-X Part 6: PCBs finished, fun with i2c bus, and how to keep the lid open
----
Author: Dileep
----
Date: April 30, 2016
----
Tags: all open-hardware open-source linux novena software NSA hacking hacker electronics cryptography security machine laptop DIY
----
Text:

(image: full_PCB.jpg link: content/0-home/028-Project-Novena-X-part-6/full_PCB.jpg width: 800 caption: Three circuits in one PCB layout. Complexity measured in number of Saturdays lost.)

In my [previous Novena-X post](http://rightshift.info/starterkit/home/Project-Novena-X-part-5) I detailed my plans for a top LCD ecosystem, involving a new board that accepts wires from the LVDS breakout board (lines having to do with USB, Power, and i2c bus), and interfaces with various other display devices, be they character LCD modules, e-ink displays, or a webcam. In order to minimize the number of PCB print jobs that I'd need to send out, as well as make the layout more rectangular, I thought I'd combine the two circuits into one PCB layout. The result (which was a long time coming) is what you see above.

# Changes, and the new board

The circuit schematics, even for the old board, have had to be modified. I am using Atmel's [ATmega32U4](http://www.atmel.com/devices/atmega32u4.aspx) microcontrollers on all the PCBs, but intend to use the [Arduino](https://www.arduino.cc) bootloader on all of them. This requires certain pins (```PB7```, ```PD5```, ```PF7```) to be left unconnected, and requires pin ```PE2``` to be pulled down to ground through a ```10K``` resistor. The new schematic (for the old and new circuits) can be found below.

(image: laptop_kbrd.jpg link: content/0-home/028-Project-Novena-X-part-6/laptop_kbrd.pdf caption: Full schematics created with eeschema, click for pdf)

Page two of the schematic pdf file shows the new LCD ecosystem circuitry. This board has to be fed 7 lines from the LVDS header breakout board (including USB lines and the i2c bus). It houses two Atmega32U4 chips, one of which is hooked up exclusively to drive Seeedstudio's [e-Paper shield v2](http://www.seeedstudio.com/wiki/Small_e-Paper_Shield_V2), which in turn will drive a 2.7 inch e-ink panel from the same company. The other MCU serves double duty. It interfaces with my NHD-0440AZ-FL-YBW [character LCD module](http://www.newhavendisplay.com/specs/NHD-0440AZ-FL-YBW.pdf) (note the change from the Seiko M4024), as well as an SMA connectorized nRF24L01+ [2.4 GHz radio module from Sparkfun](https://www.sparkfun.com/products/705). The SMA connector can be extended to an antenna which could be mounted anywhere on the case. I toyed with the idea of adding GPS and HAM radio chips, but decided to stop somewhere in the interest of being done. GPS would have drained a lot of power anyway, and would require line of sight with the satellites to work.

As for the i2c bus, I had loads of options. There are so many fun i2c slave devices that my Novena could talk to using just two wires. I took a look at [Josh Datko's](https://datko.net/) [Cryptoshield](https://www.sparkfun.com/products/13183), and decided to throw in a TPM chip (AT97SC3205T), and an AES-128 encrypted EEPROM (ATAS132A). I also threw in a BME280 [atmospheric sensor chip](https://www.sparkfun.com/products/13676) for kicks. I have confirmed that the native i2c addresses do not clash with any other i2c device on the Novena motherboard. The two ATmega32U4s' communicate with the Novena as USB devices through a USB hub chip (TUSB2046BVFR), which is also scheduled to be connected to a USB [webcam](https://www.sparkfun.com/products/11957). The remaining USB port on the hub could be exposed to a USB header mounted on top of the case. Next, layout and printing! 

# Oshpark is your best friend

(image: footprint_check.jpg width: 800 caption: Checking to see if I paired the right footprints to the right chips. Always a hassle.)

I ordered the components before printing the PCB. This allows me to print the solder mask layers onto regular paper, to check if the footprints match. Next, I uploaded the PCB gerber files to [my favorite PCB printing service](https://oshpark.com/). Since this is a two layer board spanning 5.57x1.66 inches, and Oshpark only prints these in multiples of three, I got three copies printed for USD 46.25. The drill they use to make the edge cuts is about 0.1 inches wide. This is why I demarcated the boundary between the three PCBs' with lines on the silkscreen layer. I had to cut them out later by myself using a fret saw.

(image: PCBs.jpg width: 800 caption: Purple PCBs from Oshpark. Leave a comment if you'd like me to ship one of the uncut boards to you.)

The results look pretty good.

(image: eco.jpg width: 800 caption: LCD ecosystem. All of this goes behind and around the main LCD screen.)
(image: eco2.jpg caption: Keyboard controller fits snugly beneath it.)

The PCB design files (including schematic, footprints, libraries, gerber files, and BOM) can be found on my [git repository](https://github.com/dileepvr/novenaX_kicad). I will also link to the [list of components here](http://rightshift.info/starterkit/content/0-home/028-Project-Novena-X-part-6/laptop_kbrd_BOM.csv). Some of the chip footprint choices may have been bad in hindsight (some footprints are rarer than others). Feel free to modify to heart's content (subject to CERN's Open Hardware License v1.2).

# Brass is ridiculously easy to work with

(image: brass01.jpg width: 800 caption: Hinges and wingnuts to keep the lid open.)

The previous post showed the general form of the laptop finally take shape, but the piano hinge that allows the lid to open/close is free to rotate in its full range. I needed a mechanism that can hold the lid open to arbitrary angles. Chatting with the staff at the machine shop resulted in a clever hack. Why not use the extruder rods that are already mounted on either side of the chassis?

(image: brass02.jpg caption: Extruder rods to the rescue.)

Low-profile shoulder screws from [McMaster-Carr](http://www.mcmaster.com/#low-profile-head-shoulder-screws/=127ogur) with a shoulder length of 1/16 inches allowed me to mill out bolts that swung freely on the 4.2 inch long, quarter-inch thick brass rod. A wingnut, when oriented right, fits right into the groove on the bottom extruder rod when the lid is closed.

(image: brass03.jpg width: 800 caption: Lid goes up, lid comes down. Never a miscommunication.)

I am now at the stage where I'll have to start mounting some electronics into the chassis. I think I'll work on the LCD ecosystem first, since I have all the components for the top half ready to go (soldering party!). For the bottom, I'm still waiting on the battery controller board. There is right now, a community driven effort to get some printed and assembled. Head over to the [forums](http://www.kosagi.com/forums/) for more.

(image: brass04.jpg width: 800 caption: BAM!)
