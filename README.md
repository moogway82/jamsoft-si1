# jamsoft-si1
Jamsoft SI-1
---
The Jamsoft SI-1 is a recreation of the [never-released AMSTRAD SI-1](https://en.wikipedia.org/wiki/ZX_Spectrum#ZX_Spectrum_+2A#ZX_Spectrum_+2A) for the ZX Spectrum +2A/B. It effectively turns a +2A/B into a +3.

It was designed using the excellent schamtics from [Guesser](https://zxnet.co.uk/spectrum/schematics/) and was a great first retro project for me.

Its designed to use a regular HD 3.5" PC Floppy drive and has a READY signal simulation built in. The READY signal simulation is implemented as several of the drive manufacturers metion - counts 2 INDEX signals after MOTOR ON. I also added a debounce of the INDEX pulses as my TEAC drive showed some bounching of the first few pulses, meaning it was only counting 1 rotation.

Never tried it with an AMSTRAD FD-1 and might not work even with a special cable due to the READY signal simulation. Would probably work with a Gotek but not tried.

I've also implemented a switch to change sides of the disk or support the uPD765 head 

It doesn't feature a power supply for the floppy drive as I was very worried about overloading the +2A Power Supply as I'd read that the +3 had a beefed up supply to deal handle the floppy drive, but I think I was probably being over-cautios and it would work fine with a 'modern' (90s-00s) 3.5" PC Floppy drive.

This was my first ever PCB design and as such there are some howlers in it that I haven't had time to correct, issues are:
- Missing decoupling capacitors for the READY signal simulation logic ICs
- Decoupling capacitors that are there are not next to the ICs and just randomly scattered across the board
- It's a milimeter or too too wide and getting a bit in the way of the PSU socket. I can *just* get it to fit with a bit of wiggling.
- VCC traces are same width as signals...
However saying all that, I haven't had any issues with it up till now...

How I transfer Tape Games
---
This has worked for me for most games I try, but I've had problems with one or two (ie, Double Bubble didn't work for me):

1. Load the .tap/.tzx file in an emulator (like, FUSE) set to +3 mode
2. Pause the eumulator once loading is complete and save a z80 snapshot
3. Repeat 1-2 for another 4-5 games (I can get about 5 games on 1 side of a disk)
4. Use the amazing [Z80onDSK](https://tomdalby.com/other/z80ondsk.html) from Tom Dalby to create a .dsk image of the snapshot files, using a command like:

`z80ondsk -l thewitch.z80 -o witch snowed128.z80 -o snowed mikie.z80 -o mikie Feud.z80 -o feud games1.dsk`

5. Use [HxCFloppyEmulator](https://hxc2001.com/download/floppy_drive_emulator/) to convert to .dsk to .hfe disk image
6. Use [Greaseweazle](https://github.com/keirf/greaseweazle) to write to a floppy disk. If using a HD disk, make sure to cover the HD hold to make it a DD one. Also tell Greaseweazle to only write to first side (head 0), using a command like this:

`gw write --tracks="c=0-81:h=0" games1_dsk_d.hfe`

7. Pop disk into the speccy and hit loader, select the game you want to play from the menu and enjoy!





