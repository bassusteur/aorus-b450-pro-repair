# Aorus B450 pro repair
I was in need of a pc upgrade so i spent a while looking for used motherboards on the local used market, specifically AM4 motherboards with the B450 chipset.
I came across a listing for a **Gigabyte Aorus B450 pro** for 50 bucks so, out of curiosity as to why the price was so low, i clicked on it and checking out the description
i found out why:
> selling this motherboard because i was updating the bios and something went wrong, black screen on boot, someone could probably save it by flashing it or something like that idk how to do, i already switched to another motherboard.   
 
"must be an easy fix" i told myself, unaware of the chaos to come, _so i just bought it right away_.
I receive it the next week, and the next few are a waiting game for the other components to be delivered - now it's Thursday and i'm HYPED to get this thing working, so i assemble it and
the system _partially_ works:
- RGB lights are on
- i get a POST beep without errors
- motherboard logo screen
- debugging lights work and the VGA led is on   

What doesn't work though:
- any type of input
- the screen is literally frozen

![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/dde4f5c5-d992-4644-be69-05d249c1c656)


Something's up, and in the course of a few days i try every possible troubleshooting step ever tried in the history of ever, swapping ram stick channels, only one ram stick in at a time and
since the led is stuck on the VGA step of boot i try using 3 different graphics cards but without success... Basically this thing is useless at the moment and my guess is one of the bios chips' gone bad and dual bios didn't kick in.

![PXL_20231209_145827418](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/9e3621ea-26dc-4c49-b846-50c384326e99)


So i do the only thing any sane person would do and desolder the M_bios microchip.
"MX25U12873F" is written on it, i look up the datasheet and would you look at that.. 1.8v spi flash. son. of. a. bitch. - i dust off my rp2040 board and drop ![pico-serprog](https://github.com/kukrimate/pico-serprog) on it.  
Since it has 3.3v GPIO and i need 1.8v i can just make level shifters for each line, 3 resistor dividers for CLK, CS and SI, one transistor driven for SO and for power? 
just solder some wires on the motherboard and use its power supply, to make things easier i put it on a breakout i DIY'd a while back.

![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/2743f70c-15e5-445e-a6d1-3a8ac5169821)

![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/e2629bcd-a7dd-4b2f-bebb-d75d8171e764)
![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/d5ca06b4-5a2c-48e1-ba2b-291c80cd7778)
:(   

This didn't work, i found out later i may have accidentally killed the chip by swapping the power supply, i'm still not sure, anyway it wasn't a big loss for me since i had another chip - so i went with that, desoldered and with it on the breakout i'm ready to begin testing.   
_**Success!**_ i was able to read and write data to it, obviously i made a backup of the image that was on it and went on a quest to find a bios dump online (so many paid websites), this was hard and i didn't have much success except for a shady one extracted from the **wifi** version of the motherboard.   
![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/033f8747-be51-422e-abc4-cfdd6a84b4c5)
![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/6bb7a718-bae4-452e-947e-32ce86fee3cb)

With the firmware loaded on the chip i solder it back on, hoping for any signs of life, i short the two pwr_btn contacts then the fans spin up, the CPU led lights up then DRAM but the VGA led doesn't come on, "fuck" i thought to myself - "i'm really out of options",
EXCEPT i try one last thing in an act of desperation and solder the m_bios chip in place of the b_bios one.
![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/b55c3243-85ce-445c-8528-af8d28f6d904)
_the actual moment_   

"FINALLY", "IT WORKS", i absolutely explode with happiness as the machine comes to life and i finally am able to enter the bios with everything detected and working.

![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/25911ba3-2aed-46df-a765-5be4c638ba28)
![image](https://github.com/bassusteur/aorus-b450-pro-repair/assets/42449683/bda7b783-39e9-48e7-ab07-d6cb56923fda)

