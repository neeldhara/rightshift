Title: Project Novena-X Part 5: PCB design, front panels, and piano hinges
----
Author: Dileep
----
Date: November 30, 2015
----
Tags: all open-hardware open-source linux novena software NSA hacking hacker electronics cryptography security machine laptop DIY
----
Text:

(image: keyboard.jpg width: 800 caption: The 0wx4jf Dell backlit keyboard with no controller)

My quest to design a custom keyboard controller has progressed at a steady pace, but has forced me to redesign certain aspects of the laptop. With the term coming to an end in a couple of weeks, I should be free to get all the necessary PCB printing for this project done in one go. Hence, I am focusing on the rest of the hardware build instead of wraping up the keyboard issue by itself once and for all. On the hardware side of things, I finally know what the laptop will physically look like, and am eager to design a partial lid-opening mechanism. And after that, it's time to mount electronics!

# What a front panel needs

The Novena board has an FFC/FPC cable header on the back, which is explicitly labeled the "Front Panel" header. It is used to connect to a front-panel board in the "laptop" and "desktop" product models of Novena in the original [crowdsupply funded campaign](https://www.crowdsupply.com/sutajio-kosagi/novena). As shown in the image below from the schematic files, the header contains two separate USB lines, six FPGA ICSP pins (which can also be used for general purpose input/output (GPIO)), some speaker driving pins, as well as miscellaneous function pins.

(image: fp.jpg width: 800 caption: Front panel header schematic on the back of the Novena motherboard)

By default, the ```GPT_CMPOUT3``` pin drives a CPU activity LED, ```KEY_ROW1``` is the bluetooth association button, ```KEY_COL3``` is meant to sense when the laptop lid is open/closed, ```EPIT1_EPITO``` is meant to control a 5V power output through a regulator chip on the front panel, and ```GPT_CAPIN1``` is meant to indicate when there is an overdraw of current from the regulator. The ```CHG_PWRSWITCH``` goes to the power button. The ```TS_ANA``` pin is a spare analog readin pin from the STMEP811 chip (the one controlling our touchscreen panel from the [previous post](http://rightshift.info/starterkit/home/Project-Novena-X-part-4)). This is unused, and we'll need to monkey with the kernel drivers to use it. I intend to stick an ambient light sensor on it so I can script an automatic LCD backlight dimmer. The plan is to design a PCB with a microcontroller on it, that acts as a translator between the bare keyboard resistor matrix and one of the USB ports.

(image: front_panel.jpg width: 800 caption: Planned front panel top layer layout)

I envision a printed circuit board (PCB) that sticks onto the keyboard pins on top, with the power button, the bluetooth association button, and the microcontroller reset button on the top layer, along with some indicator LEDs and the ambient light sensor. I'll connect the six FPGA lines to LEDs as well for GPIO testing purposes. The PCB should have two FPC/FFC cable headers (along with all necessary chips) on the bottom layer. One 30-pin FFC header to accept a connection from the motherboard front-panel header, and another 3-pin FFC header to connect to a separate lid-sensor PCB with a pushbutton on it that gets pressed whenever the laptop lid is closed.

So I pulled up [KiCaD](http://kicad-pcb.org/), which is a suite of open source electronics design software modules, and started laying out a circuit involving an ATMEGA32u4 chip. I highly recommend the [Contextual Electronics KiCad tutorial](https://www.youtube.com/watch?v=iTyi3RvNoB0) series on youtube if you want to learn how to do this by yourself. The schematic below shows how I intend to use various pins, and which ones I intend to not use. Note the use of the CD4051 multiplexers to read voltages from the keyboard matrix pins into the microcontroller.

(image: laptop_kbrd.jpg link: content/0-home/027-Project-Novena-X-part-5/laptop_kbrd.pdf caption: Front panel schematic created with eeschema, click for pdf)

# PCB tetris

The Dell 0wx4jf keyboard requires a non-standard pin recepticle. I had to create my own PCB footprint by physically measuring the dimenions of the darn thing.

(image: pins.jpg width: 800 caption: Physical dimensions and footprints)

The schematic in the previous section reveals the function of all the pins. I had to manually determine the resistor matrix connectivity by hand, to determine the following table of keymappings.

(image: keyboard_pinout.jpg link: keyboard_pinout.jpg caption: The 0wx4jf keyboard resistor matrix)

The table indicates the pins that get shorted when ever a particular key is pressed. For example, the key 'z' results in pins 3 and 16 being shorted to each other. I discovered that they aren't literal shorts, as they still have significant resistances between them even with key presses. Next, I started to lay the physical component footprints out on a 2-layer PCB, and very quickly realized a problem.

(image: laptop_kbrd_pcb.png width: 800 caption: PCB layout created using KICAD)

I was planning to use [OSH Park](https://oshpark.com), the community based PCB printing service, to get this done. They however, charge USD 5 per square inch. The yellow lines above are edge cuts. The top right sector of my design is empty, which counts as wasted space that I'll have to pay for. I figured that it is better to try and populate that with components from other PCBs that the project will need, so I'd end up with a proper rectangle for print in the end.

# Extra LCD plans

In the [first post](http://rightshift.info/starterkit/home/Project-Novena-X-part-0) in this series, I had indicated that I wanted the laptop to have secondary LCDs besides the main TFT one (for HUD, status, and other miscellaneous displays). I have since settled on an e-ink screen on the side and the [Seiko M4024 4x40 character LCD module](https://www.eio.com/admin/images/Downloads/SeikoChar.pdf) on top.

(image: M4024.jpg width: 800 caption: The Seiko M4024, 4x40 character LCD module)

This will leave some empty space in the top right corner of the laptop screen space, which I intend to stick a camera into. What I have to work with are all the pins on the 50 pin FFC cable that originates from the Novena LVDS header and ends up plugged into the perf board in the [LCD post](http://rightshift.info/starterkit/home/Project-Novena-X-part-3). Those pins did have power lines, and a 4-wire USB connection. In order to deal with this with the minimum amount of work possible, I plan to fan that out to three USB ports using a HUB chip, and treat both the LCDs and the camera as plug-and-play USB devices. The camera can be any old webcam, and for e-ink I think I'll go with [Seeedstudio's arduino shield](http://www.seeedstudio.com/wiki/Small_e-Paper_Shield). And for the Seiko module, I think I'll use the arduino [Enhanced Liquid Crystal library](http://playground.arduino.cc/LCD/EnhancedLiquidCrystal), which can handle the dual HD44780 chips on the Seiko module. So that, along with [lcdproc](http://lcdproc.omnipotent.net/) on the computer end should do nicely.

(image: newboard.jpg caption: Design for the top LCDs ecosystem)

# Piano hinge, and the form reveals itself

Working the steel piano hinge on a mill so I have through holes and counter sinks for 8-32 screws was a bit of a pain, as the hinge was quite thin and tended to get bent a lot. But that wasn't irreversible. These usually tend to work just fine once they are screwed into whatever they were suppose to attach to.

(image: chassis0.jpg width: 800)

The biggest issue was to pick a good amount of spacing for a sheet of barely compressed neoprene rubber to fit inbetween the top and bottom segments of the laptop as shown below. I didn't want the lid to shut with a clang, and a border layer of neoprene should prove an adequate cushion. There was still some machining left to be done at this stage to ensure that the lid opens to nearly 180-degrees. Note that the piano hinge is on the inside now.

(image: chassis1.jpg width: 800 caption: Space for neoprene rubber border)

I had to mill out full horizontal slots for the 50pin FFC cable to pass between the two segments freely. I could have restricted the width, had I advance knowledge of the region the cable is most likely to camp in throughout the opening/closing motion.

(image: chassis2.jpg width: 800 caption: Slots for FFC flex ribbon cables)

But it was good to see the whole thing finally take a recognizable shape. Next up, I'll need to find a way to use the 80/20 extruder rods on the sides to figure out a contraption that would allow me to open the lid partially up to arbitrary angles and lock it in position. More on that in the next post.

(image: chassis3.jpg width: 800 caption: Final form takes shape)
