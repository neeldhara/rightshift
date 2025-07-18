Title: Project Novena-X Part 0: Assembling an open hardware laptop
(and regularly documenting progress)
----
Author: Dileep
----
Date: June 28, 2015
----
Tags: all open-hardware open-source linux novena software NSA hacking hacker electronics cryptography security machine laptop DIY
----
Text:


(image: novena-id-pvt2a.jpg width: 1000 caption: sourced from kosagi.com)

Ever since I received my Novena motherboard from Bunnie and Xob's (link: https://www.crowdsupply.com/sutajio-kosagi/novena text: crowd funding campaign popup: yes), I've been procrastinating on doing anything with it. But now that a summer is upon me, and I am fully funded by a research grant with plenty of time to spare for esoteric hobbies, why not resurrect this blog with a blast!

# What am I doing exactly?

I've been meaning to get a new mobile machine for some time now. My last laptop was a top-heavy Alienware m15x, which managed to satisfy my much younger sensibilities from 10 years ago. My needs however have evolved, and all I look for in a mobile machine is a dumb terminal. A device that has great connectivity for all sorts of wireless protocols (wifi, bluetooth, and fully programmable RF tranceiver), environment sensors (accelerometer, temperature and pressure), and really good software and hardware security features (full disk encryption, duress alternate boot, duress erasure, dynamic switching of MAC address and other fingerprints, TPM?). And yet, one that isn't meant for computationally taxing tasks, but is merely meant to serve as a user interface when connecting to more complicated machines (which will lend it some longevity). In other words, a custom hacker-style laptop for the security conscious, tech-savvy individual. Needless to say, nothing on the market fits this. The proper way to go about this would be to buy what is known as a barebook, or a barebones laptop. But those have fallen out of favor in the free market these days. So I thought I'd go for the more expensive but fun option instead.

(image: Open-source-hardware-logo.png class: floated caption: sourced from wikimedia commons)

I am at a particular junction in my academic life where I have a reasonable amount of time, some funds, and access to facilities and equipment (a machine shop, an electronics shop, and loads of expert advice). And my preferred means of learning something new is to try and document it tutorial style. And I jumped onto the Novena bandwagon as soon as I heard that an open hardware laptop had appeared on a crowd-funding website. No TPM, but hey, you can't have everything.

# Why is this going on a personal blog, and not on the (link: http://www.kosagi.com/w/index.php?title=Novena_Main_Page text: Novena wiki popup: yes)?

Novena is currently being supported by a small community. The funding campaign had a little over 1000 backers, and the (link: http://www.kosagi.com/forums/ text: forums popup: yes) have about 300 registered users. Needless to say, that everyone in this group is rather skilled and knowledgeable about electronics and software. The project has become a niche, and looks daunting to any novice who might otherwise have been interested in it. This is not necessarily a problem, as Novena was always meant only for developers, and not everyday users. I intend to learn a lot by first-time experience throughout this project, and I intend to create a comprehensive, idiot-proof guide that I myself would find useful. Such a guide would be too basic and redundant on any official Novena developer forum, but would be right at home here on Rightshift.

# Okay. Some pompous smart-aleck is playing with computers on the internet. Why should you care?

Because if you don't, then as Tyler Durden put it, "_The things you own, end up owning you_." We are rapidly being dominated by technology that is completely opaque to us. Our web habits are being tracked, our shopping choices are being recorded, and the glass slabs in our pockets can download U2 albums without our consent. If things continue as they are, the **"Internet of Things"** era will consume what little agency we have left in understanding the systems that affect our everyday lives.

(image: NSA_TAO.jpg width: 800 caption: sourced from arstechnica, who in turn got it from Der Spiegel)

This sounds like the paranoid ravings of a conspiracy nut, and it would have been, up to about 6 years ago. But it all turns out to be worse than imagined. Companies DO install (link: http://www.theguardian.com/technology/2015/feb/20/lenovo-apologises-adware-removal-instructions text: malware onto their machines popup: yes) that is designed to bypass a crucial SSL secure authentication protocol. The American agency NSA (link:
http://arstechnica.com/tech-policy/2014/05/photos-of-an-nsa-upgrade-factory-show-cisco-router-getting-implant/ text: intercepts shipments popup: yes) and (link: http://www.theverge.com/2013/12/29/5253226/nsa-cia-fbi-laptop-usb-plant-spy text: tampers with hardware popup: yes) on electronic goods being transported to customers (link: http://www.extremetech.com/computing/173721-the-nsa-regularly-intercepts-laptop-shipments-to-implant-malware-report-says text: around the world popup: yes). And the famed Van Eck Phreaking technique is real and feasible: (youtube: https://www.youtube.com/watch?v=5N1C3WB8c0o#t=17m32s width: 600 height: 400)

The only solution is to try and actively educate oneself in the inner workings of the technology one comes to rely on. Naturally, this has an unwinnable victory condition, but any small effort pays huge dividends. Even cursory experience with such systems can change they way we think about technology, and how we interract with it, and what we expect out of it. Therefore I implore everyone, especially younger readers, to dedicate a trifle amount of time every week learning to code, or program an Arduino, or even reading up on cryptography. You'd be surprised at how addictive this can get.

# So, whats the plan?

Basically, I expect to put up posts semi-regularly (once a fortnight, maybe) about Project Novena-X. I have most of the components gathered through purchases and salvage raids into orphaned/abandoned recycle bins:

(image: components.jpg)

 ... and have a rough concept of the end product in mind:

(image: concept.jpg)

I intend to make fairly detailed posts with deliberate digressions to cover as many topics as I can. For example, the next post (Part-1) will likely be about dowloading the Novena bootloader onto an SD card, which can easily devolve into discussions about signature verification and a general section on what bootloaders are. Part-2 will deal with installation of Linux, which can cover the history of Linux, a segment on distributions, and some fun facts about full disk encryption. And so on. Eventually, I hope to be talking about milling a metal chassis and chemically etching the Novena logo onto it whilst ranting about Faraday cages, skin depth, and FCC E&M emissions cerficiations.

If you've read this far, then hopefully I can convince you to follow my progress, even if you aren't concurrently replicating my steps in your own workshop. I am excited to begin, and will try my best to share that excitement with you.


## Further reading/viewing:

If this piqued your interest, here's some links to materials that you might also find intriguing:

- The NSA ANT catalog <https://en.wikipedia.org/wiki/NSA_ANT_catalog>
- The wikipedia entry on Open hardware: <https://en.wikipedia.org/wiki/Open-source_hardware>
- The Neo900 project (an open hardware smartphone in development) <http://neo900.org/>

And for the more technical minded:

- A beautiful Defcon talk on SDR (software defined radio) <https://www.youtube.com/watch?v=ZuNOD3XWp4A>
- Another defcon talk on RF retroreflectors <https://www.youtube.com/watch?v=mAai6dRAtFo>
- And another one on PCIe <https://www.youtube.com/watch?v=OD2Wxe4RLeU>
- And another one on a hack of Qubes OS <https://www.youtube.com/watch?v=EFsoCr589GI>

