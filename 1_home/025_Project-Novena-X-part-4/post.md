Title: Project Novena-X Part 4: Resistive touchscreen as trackpad, compiling kernel, and some keyboard considerations
----
Author: Dileep
----
Date: October 04, 2015
----
Tags: all open-hardware open-source linux novena software NSA hacking hacker electronics cryptography security machine laptop DIY
----
Text:


(image: promate.jpg width: 600 caption: Promate 3" Glass Panel Digitizer, sourced from athomemarket's ebay page)


A sequence of unfortunate but fruitful distractions have resulted in the end of summer arriving well before my laptop took shape. I might be talking about some of those distractions on this very blog, or other forums. What this means for Project Novena-X is simply that my updates will be few and rare, since school is going to keep me busy. I still want to get to completion by the end of the year. But it never really ends, right?

# Touchscreen as trackpad

Every laptop needs a trackpad. If one disassembles a laptop, one will retrieve a trackpad with around 8 to 10 (or more) pins. Quite a few of those are for button presses. The fundamental pointing-device behavior in these things are usually encoded in (link: http://www.computer-engineering.org/ps2protocol/ text: PS/2 popup: yes) format. So if one knows the name of the controller chip, one can figure out what the four essential pins are. My original idea was to use a trackpad recovered from a defunct laptop and stick an Arduino inbetween it and the Novena to act as a PS/2-to-USB interface. But the four unused resistive touchscreen pins on the 54-pin LVDS header on the Novena kept bothering me. And since my PixelQi LCD screen did not come with an overlay touchscreen layer (and I don't intend to stick one on it), I thought it would be great to just use the onboard touchscreen controller with a small cellphone or handheld gaming console touchscreen panel as a stand-in for a trackpad.

(image: blade_ffc.jpg width: 800 caption: Extracting solder-able wire leads to an FFC cable)

I purchased a short, 6-wire FFC/FPC jumper cable, and scrapped off the plastic to reveal the metal strips on one end. I cut off two wire leads at the other end to make sure that the 6-wire cable will fit in the 4-wire slot on the LVDS header. Next, I acquired a Promate 3" 4-wire resistive touchscreen, and soldered its four leads onto the exposed metal strips on the FFC cable.

(image: solder_ffc.jpg width: 800 caption: When soldering FFC cable leads to other flat surfaces, a bit of scotch tape is recommended)

Next, I just hooked the cable up in the vacant space on the LVDS port, as shown. I wouldn't worry about polarity of the pins as long as the X and Y axis pins are interleaved (they are for the Promate module). All axis swapping and rotating can be handled in software during calibration.

(image: 4wire.jpg width: 800 caption: Two FFC cables, one port)

With all the connections in place, I then booted the machine up aaaand ..... NADA!

# Why things don't always "just work"

**This section might not be relevant if you are using a later version of the mainline kernel than I was. But I'll put this here for posterity's sake.**

A touchscreen controller has a simple task. First, apply a voltage across the positive and negative X-axis pins (XP, XM), and read the voltage on the positive Y-axis pin (YP). Then apply a voltage across the YP and YM pins, and read the voltage on the XP pin. Then after that, report the two voltage readings to the linux kernel (through some bus). Rinse and repeat a bunch of times every second. The kernel then interpretes these voltages as coordinates, or button presses, but only if the kernel is expecting that particular chip on that particular bus to send in such data. Novena uses an STMPE811 chip, which communicates to the main processor via the i2c bus, and registers itself as, among other things, a touchscreen controller. The touchscreen controller module is labelled ```stmpe-ts```. You can see a reference to it in the ```arch/arm/boot/dts/imx6q-novena.dts``` device tree file in the kernel source.

```
     stmpe811@44 {
                compatible = "st,stmpe811";
                reg = <0x44>;
                #address-cells = <1>;
                #size-cells = <0>;
                irq-gpio = <&gpio5 13 GPIO_ACTIVE_HIGH>;
                id = <0>;
                blocks = <0x5>;
                irq-trigger = <0x1>;
                pinctrl-names = "default";
                pinctrl-0 = <&pinctrl_stmpe_novena>;
                vio-supply = <&reg_3p3v>;
                vcc-supply = <&reg_3p3v>;

                stmpe_touchscreen {
                        compatible = "st,stmpe-ts";
                        st,sample-time = <4>;
                        st,mod-12b = <1>;
                        st,ref-sel = <0>;
                        st,adc-freq = <1>;
                        st,ave-ctrl = <1>;
                        st,touch-det-delay = <2>;
                        st,settling = <2>;
                        st,fraction-z = <7>;
                        st,i-drive = <1>;
                };
        };
```

However, the output of ```> lsmod | grep stmpe``` was null. It would appear that at the time of this writing, the mainline ```novena-linux``` kernel (link: http://www.kosagi.com/forums/viewtopic.php?id=242 text: hadn't been compiled with the ```stmpe-ts``` module enabled popup: yes). So I could either wait for Xobs to finish his next release cycle, or compile the module into the kernel myself.

We have covered cloning the kernel git repository in earlier posts in the context of device tree manipulation. The full procedure for compiling the kernel can be found (link: http://www.kosagi.com/w/index.php?title=Novena_linux-kernel text: here popup: yes). I would use four threads instead of two, and would use a fan to actively cool the CPU heatsink if this were being done on the Novena itself, but its all there. That procedure generates four ```*.deb``` package files ```(linux-libc-dev*.deb, linux-headers-*.deb, linux-firmware-image-*.deb, linux-image-*.deb)``` in the parent directory of the current one, which can be installed using the ```> sudo dpkg -i <NAME-OF-PACKAGE-FILE>``` command. But since we are using a special build, there are a few things to take care of (besides backing up the contents of the ```/boot``` directory).

One, be sure to modify the ```imx6q-novena.dts``` device tree file to match the previous posts, so we can still use our LCD screen.

Two, open ```arch/arm/configs/novena_defconfig```, and make the following modifications:

```
CONFIG_TOUCHSCREEN_USB_COMPOSITE=m           ->      CONFIG_TOUCHSCREEN_USB_COMPOSITE=y
...
# CONFIG_TOUCHSCREEN_STMPE is not set        ->      CONFIG_TOUCHSCREEN_STMPE=m
```

This should ensure that the module file ```drivers/input/touchscreen/stmpe-ts.ko``` gets generated.

And lastly, after generation and installation of the four ```*.deb``` package files, regenerate the ```/boot/uInitrd``` image file and update the ```/boot/uEnv.txt``` file accordingly. I would use this script:

```
#!/bin/sh
mkimage -A arm -O linux -T ramdisk -n "Initial Ram Disk" -d $1 /boot/uInitrd
uInitrd_size=$(wc -c "/boot/uInitrd" | cut -f 1 -d ' ')
initrd_addr_r=$(printf "0x%x" $(((0x11ff0000 - uInitrd_size) & 0xffff0000)))
echo 'rmlcd=true\nkeep_lcd true\npreboot=usb start\nstdout=serial,vga\nstderr=serial,vga\nbootargs=resume=/dev/mapper/crypt-swap console=tty0,115200' > /boot/uEnv.txt
echo 'earlyhook=if test "$rootdev" = "PARTUUID=4e6f7653-03"; then setenv rootdev /dev/mapper/crypt-root ; fi\nfinalhook=setenv console-bootarg tty0; if test "$rootdev" = "/dev/mapper/crypt-root"; then setenv initrd_addr_r '${initrd_addr_r}' ; fatload ${bootsrc} ${bootdev} ${initrd_addr_r} uInitrd ; setenv bootargs resume=/dev/mapper/crypt-swap root=/dev/mapper/crypt-root console=tty0,115200 ; fi' >> /boot/uEnv.txt
```

It accepts one input argument, which should be the newly generated ```initrd.img-*``` file, usually located in ```/usr/share/linux-novena/```. I'd copy it onto the ```/boot``` directory and replace the old version of the same. Now, if we reboot, and execute ```> sudo modprobe stmpe-ts```, followed by ```> lsmod | grep stmpe```, we should be able to verify that the touchscreen module is now loaded, and the touchscreen panel should be working ... a bit wonkily ...


# Calibration

Since we don't want to manually ```modprobe``` the module every time we boot, it is prudent to just add the line ```stmpe-ts``` to the end of the ```/etc/modules``` file. In order to calibrate the touchscreen, I had to use the ```xinput_calibrator``` program (available via ```aptitude```). I also needed a pointy stylus and a square grid reference in the background of the transparent touchscreen panel.


(image: grid.jpg width: 800 caption: The calibration involves taping the touchscreen at four points on the vertices of a rectangle)

This spat out some text that was supposed to be the contents of a new file named ```/usr/share/X11/xorg.conf.d/99-calibration.conf```. However, I found that there was an error in the program output. This is what worked best for me in that file:

```
Section "InputClass"
	Identifier	"calibration"
	MatchProduct	"stmpe-ts"
#	Option	"Mode"		"Relative"
	Option	"ButtonMapping"	"0"
	Option	"Calibration"	"1213 3506 3551 1205"
	Option	"SwapAxes"	"1"
EndSection
```


Note that button mapping is set to zero. I don't want my taps to be interpreted as clicks. Note also that the Relative-mode option line has been commented out. The trouble is that every point on the touchscreen has been mapped to a point on the screen, since touchscreens are supposed to work that way (they are usually overlayed on the screen). So all coordinates from a touchscreen module are absolute coordinates. A trackpad however sends relative coordinates. Swiping across a trackpad in some direction with your finger will cause the mouse pointer to move in that general direction from its current location. However, on a touchscreen, the pointer first teleports to the location on the screen that has been mapped to the first point of contact during the swipe, and then proceeds to move in the requisite direction. Uncommenting that option line doesn't seem to solve the problem, and scrambles the calibration in the process. I will try and find a solution to this eventually. But the results are quite satisfying.

(youtube: https://www.youtube.com/watch?v=c-HQF5whs5I width: 600 height: 400)

# Backlit keyboard

(image: keyboard.jpg width: 400 caption: The 0WX4JF thinkpad backlit laptop keyboard, sourced from Dell's product page on Amazon)

Laptop keyboards are a strange class of beasts. They don't come with controllers themselves. They are usually just a 2D matrix of resistors, with the keys acting as shorting switches. The backlit keyboard that I have chosen (0WX4JF) is even stranger because of its unusual connector type.

(image: keyboard_pins.jpg width: 800 caption: There are 33 pins on the left, 4 in the middle for the trackpoint joystick, and 3 on the right for the backlight LEDs)

I managed to use a multimeter and map out the 2D matrix with the 33 pins on the left. Here are my results:

(image: keyboard_pinout.jpg width: 800 caption: The 2D matrix)

If you want to verify this yourself, just make sure to not check for shorts, but measure the resistance between pins. There is significant amounts of resistance in every arm of the matrix (presumably to avoid large currents). The middle 4 pins are for the trackpoint joystick. They aren't USB or PS/2. They are literally leads from the joystick. I applied 5 Volts across the leftmost and the rightmost leads among the four, and measured a change in voltage on the other two on the order of about 20 mV (positive or negative) when the trackpoint joystick was depressed in canonical directions. The three rightmost pins are for the LED backlight. They go as Vcc, Control, and GND (from left to right).

Right now, I am planning to design and etch/print a custom PCB with exposed long leads, that can be epoxied face-to-face onto the keyboard's pins. This PCB could hold an ATMEGA32u4 microcontroller, which can act as a USB device (keyboard+mouse combo), along with some parallel-in-serial-out shift registers. Reading the analog voltage values from the trackpoint joystick leads will be computationally slow. So I might need to use a pair of delicately biased amplifiers. To communicate with the motherboard, it could accept a 30 pin FFC cable from the front panel breakout header on the back of the board.

(image: fp.jpg width: 600 caption: The front panel header on the back of the Novena board conveniently has two USB ports)

This would allow me to put the main power, reset, and case-close-detect buttons on the PCB, as well as status LEDs. I have observed people online claiming that AVR MCUs are a bad idea due to them being slow. But this is for a human interface. How much speed will one need??
