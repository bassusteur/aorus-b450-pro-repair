# Aorus B450 pro repair
I was in need of a pc upgrade so i spent a while looking for used motherboards on the local used market, specifically AM4 motherboards with the B450 chipset.
I came across a listing for a **Gigabyte Aorus B450 pro** for 50 bucks so, out of curiosity as to why the price was so low, i clicked on it and checking out the description
i found out why:
> selling this motherboard because i was updating the bios and something went wrong, black screen on boot, someone could probably save it by flashing it or something like that idk how to do, i already switched to another motherboard.   
 
"must be an easy fix" i told myself, unaware of the chaos to come, _so i bought it right away_.
I receive it the next week, and the next few are a waiting game for the other components to be delivered - now it's Thursday and i'm HYPED to get this thing working, so i assemble it and
the system _partially_ works:
- RGB lights are on
- i get a POST beep without errors
- motherboard logo screen
- debugging lights work and the VGA led is on   

What doesn't work though:
- any type of input
- the screen is literally frozen   

Something's up, and in the course of a few days i try every possible troubleshooting step ever tried in the history of ever, swapping ram stick channels, only one ram stick in at a time and
since the led is stuck on the VGA step of boot i try using 3 different graphics cards but without success... Basically this thing is useless at the moment and my guess is one of the bios chips' gone bad and dual bios didn't kick in.


So i do the only thing any sane person would do and decide to desolder the M_bios microchip.
"MX25U12873F" is written on it, i look up the datasheet and would you look at that.. 1.8v spi flash. son. of. a. bitch. - i dust off my rp2040 board, drop ![pico-serprog](https://github.com/kukrimate/pico-serprog) on it and
since it has 3.3v GPIO and i need 1.8v i can just make level shifters for each line, 3 resistor dividers for CLK, CS and SI, one transistor driven for SO and for power? 
just solder some wires on the motherboard and use its power supply, as a breakout to make things easier i used one i DIY'd a while back.

This didn't work, i found out later i may have accidentally swapped the power supply wires and killed the chip AND i'm still not sure, anyway it wasn't a big loss for me since i had another chip, so i went with that, desoldered and on the breakout i'm ready to begin testing.   
_**Success!**_ i was able to read and write data to it, obviously i made a backup of the image that was on it and proceeded to *painstakingly* try to find a bios dump online, this was hard and i didn't have much success except for a shady one extracted from the **wifi** version of the motherboard.
With the firmware loaded on the chip i soldered it back on, hoping for any signs of life, i short the two pwr_btn contacts then the fans spin up, the CPU led lights up then DRAM but the VGA led doesn't come on, "fuck" i thought to myself - "i'm really out of options",
EXCEPT i try one last thing in an act of desperation and solder the m_bios chip in place of the b_bios one.
"FINALLY", "IT WORKS", i absolutely explode with happiness as the machine comes to life and i finally am able to enter the bios with everything detected and working.
