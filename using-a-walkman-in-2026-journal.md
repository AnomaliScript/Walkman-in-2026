# Using a Walkman in 2026 — Journal Export

- Exported at: 2026-07-02T14:07:46Z
- Project ID: 2332
- Entries: 37

## Entry 1
- ID: 3008
- Author: Brandon
- Created At: 2026-04-20T03:36:53Z

### Content

Today, I started my KiCad journey into making my Walkman actually happen, where I read up on the tutorial for KiCad, and did some research: it turns out the preferred MCU for my Walkman would be the **XIAO-ESP32-S3** (according to Gemini) because of its Bluetooth capability, because I would like the option to switch to my AirPods if wired earbuds got too annoying.

I looked further into the differences between the C6 and the S3 variants.
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6NjE5NiwicHVyIjoiYmxvYl9pZCJ9fQ==--5acb14f5a660d890a8a0c6090032301620a46a02/image.png)

![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6NjIzNywicHVyIjoiYmxvYl9pZCJ9fQ==--df3b9d1a01dbd6594a3cf396d8cd5d156f89692d/image.png)

WHAT? You're telling me there's more than one type of ESP23-S3?!
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6NjI0MSwicHVyIjoiYmxvYl9pZCJ9fQ==--1888b531ecb33e6241f0d58dafd018909bcd4eac/image.png)

I later learned that these differences are based on how the components will be attached to the solder board, and used this YouTube video to educate myself on how each type of manufacturing style works: https://youtu.be/UwTBCpqqacU?si=3JkgFAU-7ZSq832C (huh, this video also has Chinese captions)
I ended up choosing the SMD_PAD manufactured one, as it will allow me to hand-solder the part onto the PCB.

After this, I pursued to find a display for my Walkman replica: one that was thin and slim, but not too slim.  I finally found one on LCDC: https://www.lcsc.com/product-detail/C18198249.html?spm=wm.fly.bg.5.xh&lcsc_vid=RwBZAQAFRVcKX1JUT1heVgdTTwANAgFTFVYKBFReT1AxVlNRQVdbVVVeR1hbVTsOAxUeFF5JWAcPCwgJAhVADwUFHAICEgZIFA4DSA%3D%3D
Importing it into KiCad (specifically the Schematic) eas a nightmare.  Even through there was a gudie that helped me what to do, it still took me an hour and then some to get just the display of it on there: from using Gemini to watching Indian YouTube tutorials, I did it all, and found the schematic with two things: the ESP32 and the OLED Display screen.

### Recording Links

- https://lookout.hackclub.com/api/media/1aadc8eb-a1a8-465c-8510-a7b3c4f2bbd3/video.mp4

## Entry 2
- ID: 3151
- Author: Brandon
- Created At: 2026-04-21T03:36:40Z

### Content

Today was a full-on research day, where I learned about DACs (Digital Analog Connectors iirc?) and how they are important to translate audio data into a form where I can listen to music through a head phone jack (J1).
And because this is a music-playing device, I had to have a storage of some kind...hm....a microSD card!
Unfortunately, the poor XIAO didn't have enough room/pins to handle both the LCD display and the pins required for the MicroSD card (I also learned about MISO and MOSI pins for storage components like microSD cards).  Thus, I had to use a thingy called I2C (Inter-Integrated Circuit, I think), which is a technology that connects components together, especially peripherals.  This also meant: MORE PINS! YAY!
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6NjU0MCwicHVyIjoiYmxvYl9pZCJ9fQ==--42386255583cef83befb71258d8d41c6941cee80/image.png)
Unfortunately, it's bedtime, so I'll work on using Claude to help me know where each pins go.  I also looked up some of my first datasheets today: I'm starting to feel like a electrical engineer now!
(This is the datasheet for the pcm5102, which I'm pretty sure is a DAC that does the analog audio data translating for my headphone jack).
![Screenshot 2026-04-20 232044.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6NjU0MywicHVyIjoiYmxvYl9pZCJ9fQ==--80414a5f59351d523942ba0756acf38218e88c61/Screenshot 2026-04-20 232044.png)


### Recording Links

- https://lookout.hackclub.com/api/media/c7bf1d50-8d7d-4dc5-8d09-0e8311dab583/video.mp4

## Entry 3
- ID: 3813
- Author: Brandon
- Created At: 2026-04-25T03:59:19Z

### Content

I am so close to breaking my streak it's 11:51PM rn T-T
Today was a wild PCB designing day for me...let be begin by talking about my trying to free up a pin for my Resistor Ladder on the XIAO ESP32 S3.  Basically it needed an analog pin (ADC) but all the rest of the pins on the MCU were taken by the LCD display pins, so I had to import and look for a I2C backpack (PCF8574P) to implement in my PCB.  After spending a while adding the PCF8574P to my schematic, I connected the display pins to the PCF8574P, and rerouted the Resistor Ladder with all my switches (buttons) go to the XIAO's now-free A0 pin.  Yippee!

After, I worked on the 3.3V (XIAO and PCF8574P) and 5V (LCD) difference, because wiring those together would "wear out" the PCB, so I've heard, so I chose to add a MOSFET (BSS138) to the PCB to manage that.

There's a lot more I can talk about, but I need to turn in my journal in now, I'll talk about it more in my next entry, bye for now!
![Screenshot 2026-04-24 234217.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Nzg2OCwicHVyIjoiYmxvYl9pZCJ9fQ==--1bb725b07456aa7fa476c7e79d5b906b1aed2720/Screenshot 2026-04-24 234217.png)


### Recording Links

- https://lookout.hackclub.com/api/media/1ea78349-316f-401f-9d6a-252b5c26c8a0/video.mp4

## Entry 4
- ID: 3963
- Author: Brandon
- Created At: 2026-04-26T00:39:55Z

### Content

Review of what I did in the last journal entry, since couldn't complete the full entry due to me having to submit it before midnight (I submitted it at 11:59PM!)

_I learned all about the different pins that the Micro SD Card had, and how their pins relate to the MOSI and MISO pins in the XIAO ESP23-S3.  The data goes into the MOSI from the card, and the MISO sends out data to the card...I think.  Anyways, I used Claude to help me summarize a datasheet for the stereo ADC that I had to use to bridge between the AudioJack and the XIAO ESP23, and it turns out that TI (Texas Instruments), really wants me to put a whole slew of caps (capacitors) onto their PCM5102 to ensure "safety" or something...not quite sure of the exact reason yet...and after getting the news that I had to place a bajillion caps on there, I signed off for the night.  
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODE3NywicHVyIjoiYmxvYl9pZCJ9fQ==--5c11459681034463ffcd255508e5e989bda72507/image.png)
And that is where we continue my Walkman journey today..._

Continuing where I left off yesterday night, I had a hard time connecting the rest of the pins and learning about the audio stereo ADC component that I was working with (specifically, the PCM5102).  **This was because I had to work on my PCB with my battery-deficient laptop, where it almost constantly had to be connected to a power outlet, and I even forgot to bring my mouse!**
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODE4MiwicHVyIjoiYmxvYl9pZCJ9fQ==--d89cee07e4e239161674574eb0b974a3bfe840ba/image.png)

What will I do without my precious right-click and scroll-wheel? T-T  (For context about why I didn't have access to my desktop is because I was volunteering at a jazz music festival all-day today)

Thus, I accomplished less than what I hoped for.
During this session, I also learned about "bypass capacitors", which are mechanisms where a capacitor is placed between a GND (ground) point and intersection where power is flowing to the pin (in this case, the CPVDD, DVDD, and AVDD pins ) in order to manage power "spikes" that would happen that result from turning switches on and off.
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODE3MiwicHVyIjoiYmxvYl9pZCJ9fQ==--9a1ac9db65c43f097752d1b2c245548e9175c00a/image.png)

Luckily, I finally ended up with my first version of the (what is think is the) entirety of the schematic, now I just have to check it!  (Ugh, checking...)

### Recording Links

- https://lookout.hackclub.com/api/media/7c59ccf2-c480-4df7-b77c-4ef2a79f002e/video.mp4

## Entry 5
- ID: 3987
- Author: Brandon
- Created At: 2026-04-26T03:27:34Z

### Content

This time, I was pressed for time and I only could ask Claude for the BOM about what specific materials and component models I should get for the resistors, AudioJack, capacitors, etc for all the stuff that I was going to need to solder onto the board.

Claude gave me the difference between THT and SMD socket components, which led me to make some decisions (as I had some experience with soldering before through my robotics club, I thought that I would be able to hit them up for some soldering help for SMD soldering to help preserve space on my PCB).
![Screenshot 2026-04-25 224140.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODIzOSwicHVyIjoiYmxvYl9pZCJ9fQ==--5666e8714ae77b8935ec3d6917b1eac169265b54/Screenshot 2026-04-25 224140.png)


### Recording Links

- https://lookout.hackclub.com/api/media/c29a6eed-b1fe-4980-970e-7d8049d6ec55/video.mp4

## Entry 6
- ID: 3991
- Author: Brandon
- Created At: 2026-04-26T03:46:02Z

### Content

This session was really short, because I was doing this between chores (my parents are inviting friends over all of a sudden T-T)
Anyways, I continued my research into seeing if the Molex version of the aforementioned microSD Card reader is the same as the microSD Card reader that I chose in the KiCad footprint editor: I'll have to look at KiCad's rendition of the dimensions of the microSD Card Reader in my next session.
However, I did manage to get some dimensions of the microSD Cards that are available on LCSC, a sister company of JCLPCB that share many of the same supplies and components, so I hope there's a high chance of seeing the exact component that was listed in KiCad.

![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODI0MywicHVyIjoiYmxvYl9pZCJ9fQ==--123f936c6bb1c25d919b00139865e8d6600bcd3e/image.png)


### Recording Links

- https://lookout.hackclub.com/api/media/58d2fc34-4e16-444e-9bb2-855d7b3ae880/video.mp4

## Entry 7
- ID: 4285
- Author: Brandon
- Created At: 2026-04-28T01:03:31Z

### Content

In this session, I went into the footprint editor for some of the components (in the following screenshot I inspect the microSD Card reader by molex), and sure enough, these dimensions match the ones listed in their datasheets!
![Screenshot 2026-04-27 182044.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODg4OCwicHVyIjoiYmxvYl9pZCJ9fQ==--6b199aa9b29ae9aed784150e2575818070aff9e7/Screenshot 2026-04-27 182044.png)

After that, I went through all of these components and used the Internet and Claude to search for which components would be best for my project:
- Audio Jack
- Switches (Buttons)
- Switches (Single Pole Single Throw switches)
- Resistors
- Capacitors

For example, here is the list of all the buttons that I was considering:
![Screenshot 2026-04-27 182501.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODg4NywicHVyIjoiYmxvYl9pZCJ9fQ==--716867a5f73a5b9add5de6ef8819d39177a1c843/Screenshot 2026-04-27 182501.png)

During the process of looking for resistors, I got to refresh some of my Physics class learnings by using Ohm's law to try to calculate the required Power (in Watts) that a resistor had to have in order to be suitable for different parts of my PCB.  I learned the Power Law (i.e. P = I^2 * R) by doing this, and Claude helped me go through the formulas and calculations. (Of course, I could've gotten it to just tell me what products to get, but I like to know the "why" behind technical things like this!)

I also learned about the different kinds of resistors available to me (I chose the SW_PUSH_6.0mm one):
[](url)
![Screenshot 2026-04-27 184148.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODg5MCwicHVyIjoiYmxvYl9pZCJ9fQ==--b32cf60236f9d76bd2d669956a916b6f02708473/Screenshot 2026-04-27 184148.png)

As I finished the BOM, I realized that I may not need an audio jack, because **my wired earbuds that I have in fact use the Lightning cable**...so I'll have to fix that before I move onto the PCB editor.


### Recording Links

- https://lookout.hackclub.com/api/media/3459b02a-e108-41c2-8270-5c5de9bcffd9/video.mp4

## Entry 8
- ID: 4342
- Author: Brandon
- Created At: 2026-04-28T12:22:34Z

### Content

Today I cleaned up the PCM wiring, because I made the mistake of trusting Claude to do all the thinking of telling me where to wire things for me.  Even though I gave it the pdf of the PCM 510x datasheet, it still messed up some things for my schematic.  Some intersections between wires were missing, and the direction was off in all the wiring, although Claude had gotten all the resistances and powers right for the capacitors and resistors.
Here's the real configuration of the PCM according to Texas Instruments:
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODkyNiwicHVyIjoiYmxvYl9pZCJ9fQ==--eeb3dc558e833ddaca524a71906136dbd3df7302/image.png)

This was a headache figuring this out, as I had to move other components on the schematic to make room for rewiring the PCM.

After getting that sorted out, I was unpleasantly surprised to see that I was getting errors that KiCad couldn't find my MCU's footprint (i.e. XIAO_ESP32_S3) for the PCB Editor!  I had to scour through my /Documents, and sure enough, I forgot to include the .pretty folder that was supposed to contain the footprint for the MCU.  Going back to the page where I originally got the XIAO_ESP32_S3 for the schematic (https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/#resources), I downloaded the zipped footprint file, and placed it inside the GitHub-tracked folder, so that I could continue working on it on other devices.
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODkyOSwicHVyIjoiYmxvYl9pZCJ9fQ==--c314e06b306c18d2d6bd971ec3181caaab61abfd/image.png)

After doing so, I hoped that the footprint would appear when I went int the "Assign Footprints" page, and surely enough, it was there!  I pressed F8 triumphantly, and went on to bring the last, but certainly not least, component onto the PCB editor.
![Screenshot 2026-04-27 230242.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODkzMCwicHVyIjoiYmxvYl9pZCJ9fQ==--317439f0c297eb039411b8c1c59cb34fa096dc9b/Screenshot 2026-04-27 230242.png)

...
There's going to be a lot of work to do in the next few days.
Organizing this mess will take a while.

Before I signed off, however, I placed all the components into a box-like shape, where the enclosing perimeter barely was within regulation (100mm x 100mm).  I'll have to squeeze these things tighter if I want to make this project happen!
![Screenshot 2026-04-27 230855.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODkzMSwicHVyIjoiYmxvYl9pZCJ9fQ==--dd711f9848ca271488738b0f658288a44fa79b92/Screenshot 2026-04-27 230855.png)

Also here's what the reference of the XIAO_ESP23_S3 looks like in the PCB Editor compared against the real footprint of the MCU.  Turns out they're not the same.  That's so tricky, how the refence of the MCU can appear even if the .pretty file for it wasn't imported yet!
![Screenshot 2026-04-27 230333.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6ODkzMywicHVyIjoiYmxvYl9pZCJ9fQ==--79a7e8880928e1036c9c16b6d844b311c6793f11/Screenshot 2026-04-27 230333.png)

### Recording Links

- https://lookout.hackclub.com/api/media/d9cb07e5-026a-4644-827f-7c0e6f55e56c/video.mp4

## Entry 9
- ID: 4717
- Author: Brandon
- Created At: 2026-05-01T04:41:58Z

### Content

Today was all about the PCB Editor.  I tried to move around some wiring stuff, but there's only so much I could do with only a front and back copper wiring, and I soon had thousands of vias all over the PCB, which at that point I decided to reset EVERYTHING using KiCad's "Global Deletions" tool, and selecting all the copper paths, wires, and vias.
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6OTkzOCwicHVyIjoiYmxvYl9pZCJ9fQ==--1b193c328f010838677357a56712f773dc6455de/image.png)

It was sad having to restart after I tried to make some headway into my wiring for the past 45 minutes, but it had to be done, in order to prevent more "via hell".  After I restarted, I moved the resistors to be above (farther up than) the LCD display, which simplified some wiring things.  I have to sleep now, but hopefully I can finish this wiring tomorrow and ask for someone to review it.

### Recording Links

- https://lookout.hackclub.com/api/media/f4e20d62-6b0a-4424-9013-4a711fbb8479/video.mp4

## Entry 10
- ID: 5224
- Author: Brandon
- Created At: 2026-05-03T04:49:09Z

### Content

Today I had to deal with PCB designing on my crappy laptop again because I was busy with scouting matches at the FIRST Championship in Houston (I stopped by the Hack Club booth, it was cool!)
Between bus rides back and forth from the hotel, I attempted to continue wiring my PCB together in KiCad's PCB Editor.
![Screenshot 2026-05-01 080658.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTA3OTksInB1ciI6ImJsb2JfaWQifX0=--41f046da458c332905cb3f9bd220c79f6b76303f/Screenshot 2026-05-01 080658.png)
After a bit, I was trying my best to minimize the vias and make the routes as short as I could, but at a certain point, I decided to reset all the tracks and wiring and start over...again.
When taking a break from scouting matches at the FRC Championship, I came up with the brilliant (but obvious) idea of using the schematic to determine which components should be closer to certain components.
For example, I placed the XIAO ESP23 to be in the corner of the PCB, where it's more accessible to the PCM and PCF so not as much wiring would be required.
![Screenshot 2026-05-02 200527.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTA4MDAsInB1ciI6ImJsb2JfaWQifX0=--efc021cb0a30b605798cd9a9b15e2e16936af277/Screenshot 2026-05-02 200527.png)


### Recording Links

- https://lookout.hackclub.com/api/media/081d1a5d-8d79-4d58-8523-e08076eebd12/video.mp4
- https://lookout.hackclub.com/api/media/9c58167b-8520-4ebc-a850-b66e88b1f017/video.mp4

## Entry 11
- ID: 5372
- Author: Brandon
- Created At: 2026-05-04T03:03:11Z

### Content

Today, I kept working at the track hell that I had to do...this time, the focus of my sessions was in the PCM side of things.  The PCM connects to resistors, MIcro SD, the XIAO, Capacitors, literally everything so this made my head dizzy.  Not to mention, all the pins leave to space between them to let tracks go in between them, and **they are all front-copper (red) pins!**
This is a picture of me resorting to rotate the PCM in order to try to find a better way to organize it so that it results in fewer cross-overs and via craziness (i.e. the PCM pins are closer to their destinations to a greater extent).  What you see here is what the tracks were left behind when I dragged the PCM out of the frame of the PCB in order to rotate it separate from the whole PCB chaos.
![Screenshot 2026-05-03 222950.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTEyMDQsInB1ciI6ImJsb2JfaWQifX0=--6f3292b17f64918ec92dae4bfea5100a2c374123/Screenshot 2026-05-03 222950.png)
Finally, after grueling work (not really, but it was tedious) I got a version of the PCM wiring (with less than 15 vias! yay...).
I never verified that having less vias is better for a PCB, but according to my common sense, less vias -> better
![Screenshot 2026-05-03 225528.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTEyMDYsInB1ciI6ImJsb2JfaWQifX0=--8bc561d3e7c2e05a8dcfe6e8ac5439f5e31b6b64/Screenshot 2026-05-03 225528.png)


### Recording Links

- https://lookout.hackclub.com/api/media/d54699b7-06cb-4a69-8d3b-d5952ae25e61/video.mp4
- https://lookout.hackclub.com/api/media/aa61b15c-58b1-4517-ae1a-48ab2f16fae1/video.mp4

## Entry 12
- ID: 5540
- Author: Brandon
- Created At: 2026-05-05T03:11:13Z

### Content

Today, I finally attempted to close out the tracks in the PCB design, and since I did the hard stuff before (i.e. the PCM and micro SD card pins), it was relatively easy for me to do.

What wasn't as easy, however, was running the DRC and troubleshooting every error and warning.  One of the first errors that I fixed was the overlap of these pink outlines of the components: they're called courtyards.

In my case, the two BSS components that I had had overlapping courtyards, and here's the before and after the error:
![Screenshot 2026-05-04 220401.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE1NDcsInB1ciI6ImJsb2JfaWQifX0=--08c6f551dd149ae8210f684392022b40a7c734cb/Screenshot 2026-05-04 220401.png)
![Screenshot 2026-05-04 220605.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE1NDYsInB1ciI6ImJsb2JfaWQifX0=--34adc54a22571cb0645a82d2cbf79066c4def114/Screenshot 2026-05-04 220605.png)

Moving it was a bit annoying, as I had to rewire and track every one of the tracks that were connected to it.  I looked up a way to be about to move the component only in KiCad and have the tacks connected to it update themselves, but what KiCad offered, the "Drag" tool (activated by pressing "d") didn't work very well in my PCB because of the sheer amount of track and wire action going on.

After, I noticed that I kept getting an error about "malformed Edge.Cuts" shape, and I was initially confused, until I realized that I never defined a shape for the PCB, and only defined silkscreen shapes to outline the rough size restrictions for my PCB (100mm x 100mm).  Following this, I unfortunately discovered that the XIAO-ESP23-S3's footprint was barely outside the Edge.Cuts border.  To fix this, I had to move the XIAO back into the PCB.
![Screenshot 2026-05-04 222547.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE1NDUsInB1ciI6ImJsb2JfaWQifX0=--a98285fe6fd12655d29bc6f4147e7ac55cd1dbc1/Screenshot 2026-05-04 222547.png)

I wanted to see the current version of the PCB in its 3D form: here it is as of right now!
![Screenshot 2026-05-04 225843.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE1NDQsInB1ciI6ImJsb2JfaWQifX0=--89d827b5e543f38b9b32345d0db8c270b57245f1/Screenshot 2026-05-04 225843.png)

### Recording Links

- https://lookout.hackclub.com/api/media/d5e59945-c8f8-4c8d-9821-e8e7d1448bd1/video.mp4

## Entry 13
- ID: 5680
- Author: Brandon
- Created At: 2026-05-06T03:59:44Z

### Content

Today is the day where I import my Gerber files (zipped) into JCLPCB and see how much it costs!
Of course, I chose the cheapest delivery price, and it was pretty cheap (of it may be because all of the deals I'm getting as a new JCLPCB member).
Here's me realizing that I need to get to reimport the Gerber files because I forgot to include some of the files.
![Screenshot 2026-05-05 231304.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE4NjMsInB1ciI6ImJsb2JfaWQifX0=--e07a582738bfca104d7769cdffbb59deda52c5c8/Screenshot 2026-05-05 231304.png)
![Screenshot 2026-05-05 231408.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE4NjQsInB1ciI6ImJsb2JfaWQifX0=--10b640fb9a3c0bf79d11d9fb37fef2effc9c10ca/Screenshot 2026-05-05 231408.png)
This is me ordering my last PCB project because I didn't finish the process of buying it last time.
![Screenshot 2026-05-05 232029.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE4NjUsInB1ciI6ImJsb2JfaWQifX0=--f81b7b1b18e482c0191f96f74195d813e653b894/Screenshot 2026-05-05 232029.png)
![Screenshot 2026-05-05 232422.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE4NjYsInB1ciI6ImJsb2JfaWQifX0=--e44214b435eacf871a7084f6911f0e41ba4d1e52/Screenshot 2026-05-05 232422.png)
I also exported the 3D rendering of my Walkman rn!
![Screenshot 2026-05-05 234517.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTE4NjcsInB1ciI6ImJsb2JfaWQifX0=--5b7507bb1f2a7241e148071c42350046c9f3f8e5/Screenshot 2026-05-05 234517.png)


### Recording Links

- https://lookout.hackclub.com/api/media/bdf27283-ae1d-45e6-8739-f536f6d2cbec/video.mp4

## Entry 14
- ID: 5831
- Author: Brandon
- Created At: 2026-05-07T02:45:31Z

### Content

After getting some rest last night (I got to sleep in because of AP exams), I found all the rest of my 3D models for my PCB in order to get an accurate visual representation of my PCB so that I could import it into OnShape so that I can start making a 3D printed case for it to protect it.
During my importing process, I had to go file hunting in my Walkman/ and Program Files/KiCad/ folders, because when I use easyeda2kicad, it outputs the .step 3dmodel files for the components into the Program Files/KiCad/ and I placed them into my Walkman/ folder (that is being tracked using GitHub Desktop).  I did this to maintain continuity, dunno if this is bad file management as an electrical engineer.  (Guess I'll find out the hard way later)
![Screenshot 2026-05-06 212219.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTIyOTAsInB1ciI6ImJsb2JfaWQifX0=--f413e3da828af8c68d89278e7bcf9ff1e7c57e5e/Screenshot 2026-05-06 212219.png)
![Screenshot 2026-05-06 213040.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTIyOTEsInB1ciI6ImJsb2JfaWQifX0=--3c104f3e5a81ce704d8915db2b6f4a884d3fb5d7/Screenshot 2026-05-06 213040.png)
![Screenshot 2026-05-06 213817.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTIyOTIsInB1ciI6ImJsb2JfaWQifX0=--4c1f68b3b829d9ec9357e0124f8e67423e780ec4/Screenshot 2026-05-06 213817.png)
![Screenshot 2026-05-06 215306.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTIyOTMsInB1ciI6ImJsb2JfaWQifX0=--476717d354268f6153359c1038e2ae093cc5b7a0/Screenshot 2026-05-06 215306.png)
For the SPST switch, KiCad didn't have the 3D model in its Program Files for some dumb reason, so I had to create an account for Omron [https://components.omron.com/us-en/](url) and downloaded the SPST switch 3D model directly from there (specifically, it was from the B3F series).
![Screenshot 2026-05-06 221542.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTIyOTQsInB1ciI6ImJsb2JfaWQifX0=--639548fa82240f6aa86d80d540f72e841183c0d9/Screenshot 2026-05-06 221542.png)
Here's what my PCB 3D rendering looks like now!  (Also sorry for the short journal entry yesterday: it was because I was writing up my entry at 11:58PM .-.)
![Screenshot 2026-05-06 221612.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTIyOTUsInB1ciI6ImJsb2JfaWQifX0=--284817e6394ce74c89b462b1aef71d7e19219c22/Screenshot 2026-05-06 221612.png)


### Recording Links

- https://lookout.hackclub.com/api/media/abaec749-8537-4eda-8e71-62728c9de4de/video.mp4

## Entry 15
- ID: 6201
- Author: Brandon
- Created At: 2026-05-09T03:59:42Z

### Content

So sorry but I have to use next journal entry to document my progress, the deadline (midnight) is coming up fast
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTMxNDUsInB1ciI6ImJsb2JfaWQifX0=--f4244ddc749b1e13b9570121c422fb4d120b6ef7/image.png)


### Recording Links

- https://lookout.hackclub.com/api/media/9289bfb3-3035-4c9d-a1b8-d4c7699f0ab0/video.mp4

## Entry 16
- ID: 6204
- Author: Brandon
- Created At: 2026-05-09T04:28:51Z

### Content

[This entry is for the last journal entry due to midnight closing in fast and I wanted to maintain my streak, thus the dummy Lookout Timelapse]
Diving deeper into 3D rendering inspection, I noticed that the pins on the LCD and the Audio Jack looked especially odd, and after fixing the Z axis of the Audio Jack in the 3D rendering, I went and asked Gemini what was going on with the LCD Display screen.
![Screenshot 2026-05-08 213641.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTMxNDYsInB1ciI6ImJsb2JfaWQifX0=--df14d4685eb5d5434817085eca025dbedc0464b5/Screenshot 2026-05-08 213641.png)
This wasn't my first time seeing the LCD's unique "blocky" pins compared to the other components, but I just never asked or questioned it up until this point.  Seeing that the pins just protrude through the PCB, I decided to finally find out what is actually supposed to happen with that LCD display.  Turns out, after research and looking at this [video](https://www.youtube.com/watch?v=qkb5_Wu0lgk), I couldn't believe that this LCD is supposed to be "dangling", only supported by the blocky pins that it has--well that's the way it is, I guess.
![Screenshot 2026-05-08 214419.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTMxNDcsInB1ciI6ImJsb2JfaWQifX0=--c956abbc6266fd00eff3ad144022fddaf2015ec8/Screenshot 2026-05-08 214419.png)
So after this discomforting discovery, like a good STEM student, I was concerned about the LCD display's support and the possibility of it breaking off or bending the pins (even though I going to build a case for it anyways).  This led me to the discovery of "standoffs", which are supports built for the corner holes in the LCD display.
![Screenshot 2026-05-08 233544.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTMxNDksInB1ciI6ImJsb2JfaWQifX0=--15882540e3aa2881b88ef028c3d61f63a612f0c7/Screenshot 2026-05-08 233544.png)

![Screenshot 2026-05-08 233922.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTMxNDgsInB1ciI6ImJsb2JfaWQifX0=--5a99a3d783385b2c2e7e47af080033cdf4d6869a/Screenshot 2026-05-08 233922.png)
After doing some more digging, I conveniently found a file for 3D printing these "standoffs", and given that I have a 3D printer, this worked out for me!  (I found the 3D prints [here](https://www.thingiverse.com/thing:4963899))
![Screenshot 2026-05-08 234053.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTMxNTAsInB1ciI6ImJsb2JfaWQifX0=--23856da5bba24489781e062c17c0c371af986e37/Screenshot 2026-05-08 234053.png)


### Recording Links

- https://lookout.hackclub.com/api/media/e649ba19-e280-4b08-a3d2-dc83b9d8bf2d/video.mp4

## Entry 17
- ID: 6374
- Author: Brandon
- Created At: 2026-05-10T03:48:45Z

### Content

I made my own custom "standoffs" which are supports that support the LCD display, because it needs extra vertical room in order for its pins to be connected to the PCB. I 3D printed both a "screw" and a "non-screw" version of the standoffs, to test which one would work best (standoffs are small, and the smaller a print is, the worse small details, like screw patterns, will be).
![Screenshot 2026-05-09 231951.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTM1NDgsInB1ciI6ImJsb2JfaWQifX0=--5332bb7f8415caa4ec9121fd4b5152bc17439ac4/Screenshot 2026-05-09 231951.png)
![Screenshot 2026-05-09 233715.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTM1NDksInB1ciI6ImJsb2JfaWQifX0=--38f1a260c96cdbdc81a9e6f1a4a1f704efdf10c9/Screenshot 2026-05-09 233715.png)
I sliced my custom 3D prints using OrcaSlicer (despite not having my PCB and components on hand yet because I was waiting on another PCB to be shipped first), and decided that I needed to thicken some of my standoff and nut dimensions, because the slicer gave me a reality check about how small these things actually were.
Also, I made sure to send the sliced 3D prints to my 3D printer by running to my printer and turning it on, and then running back to my computer to send the files via OrcaSlicer (and no, I did not start printing during when the Lookout was recording my session)
![Screenshot 2026-05-09 232901.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTM1NTAsInB1ciI6ImJsb2JfaWQifX0=--68cd44f4c7ea02d9a47a21c64ce28aaab589bb2b/Screenshot 2026-05-09 232901.png)
So smol they only need one popcorn 🥹


### Recording Links

- https://lookout.hackclub.com/api/media/1fb45dbc-32ee-447d-84f2-66c8de7aed37/video.mp4

## Entry 18
- ID: 6872
- Author: Brandon
- Created At: 2026-05-13T03:56:45Z

### Content

I had to review the datasheet and information about the XIAO-ESP32-S3 again with [this link](https://wiki.openelab.io/seeed-studio/xiao-esp32s3).
This session challenged me a lot, and by "challenge" I mean it reminded me that PCBs need batteries in order to run portably.  (Well duh...)
Ok, in my defense, I assumed that the XIAO having battery power management to be able to take in power without needing a middleman meant that it could store power independent of other sources, but no, I was wronggggg.
Before that, though, I did some researching about the volumes that I could play my "jukebox" at, and I found a cool table that broke down what configurations would give me different sounds (I chose 12dB gain, I want my music to be heard!):
![Screenshot 2026-05-11 211124.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTQ1OTQsInB1ciI6ImJsb2JfaWQifX0=--c35b1f8fb54bbd556063366b9e0734e7b71d7c9b/Screenshot 2026-05-11 211124.png)
I was also given a pinout diagram, which was a cool find (and useful, these things are just copy-paste :D)
![Screenshot 2026-05-11 212826.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTQ1OTUsInB1ciI6ImJsb2JfaWQifX0=--ae7ec0a427495f0a95d3c8a1b239d6927181305f/Screenshot 2026-05-11 212826.png)
Back to the main topic: I FORGOT ABOUT THE BATTERIES (for BOTH the Walkman project and the Jukebox project, for the latter of which it wasn't such a big deal).  
For the Walkman project:
After scrambling to find some way to get a wire from my battery connected back to the PCB, which has to be externally connected (from the back of the PCB) due to space constraints and aura loss (I mean, who wants to have a big brick hanging on their lanyard like that?  Remember, I want the Walkman to be as similar to Makoto's thingy as possible).  Anyhow, I tried using a Screw Terminal to connect the battery pack (LiPo) to the GND
![Screenshot 2026-05-11 223233.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTQ1OTYsInB1ciI6ImJsb2JfaWQifX0=--1c743c960496cec0efe63558e247c3223c20c908/Screenshot 2026-05-11 223233.png)
But when I placed it on the PCB editor, I saw that it was way too big for my PCB!  So I went to using a Connection, specifically a Socket (TIL why Pins are called Male, and why Sockets are called Female T-T), and it works, at least theoretically.
![Screenshot 2026-05-11 230914.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTQ2MDIsInB1ciI6ImJsb2JfaWQifX0=--4a1a9de6366f1f4eb0644d935ef82341023f6175/Screenshot 2026-05-11 230914.png)
![Screenshot 2026-05-11 231211.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTQ2MDMsInB1ciI6ImJsb2JfaWQifX0=--f92077b4117feb0b4b60da4b5a67b6ae9ad8dfe6/Screenshot 2026-05-11 231211.png)


### Recording Links

- https://lookout.hackclub.com/api/media/4b8c3a1d-cc57-4bab-ba8d-4bc89226e726/video.mp4

## Entry 19
- ID: 7857
- Author: Brandon
- Created At: 2026-05-18T20:51:27Z

### Content

Today was all about shopping, and the websites I went to were mainly:
1. DigiKey
2. Molex (which had links that lead to DigiKey sites)
3. Mouser Electronics
4. Amazon <3
After some product research, I went ahead and organized all the components on my BOM in different categories, as shown below:
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTcxMzksInB1ciI6ImJsb2JfaWQifX0=--aace7ae1b84a69911c02cc96bddfd4dce5923192/image.png)
I tried to export a BOM from the PCB Editor, but that didn't end up being too helpful: I resorted to typing the component's footprint's name into Google directly (it worked).
I also had to review a ton of the components to make sure that they were compatible with my PCB.  How did I do that? not with dimensions, but with model numbers and just eyeballing it (I am not about to check every single dimension T-T)
![Screenshot 2026-05-18 155917.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTcxODYsInB1ciI6ImJsb2JfaWQifX0=--31a3ae5ee6f042cfdd9f798f115294b47b9a4194/Screenshot 2026-05-18 155917.png)

Here are all the purchasing links of what I got so far:

[microSD card reader](https://www.digikey.com/en/products/detail/molex/0472192001/3044807)

[Conn 01x02](https://www.digikey.com/en/products/detail/molex/0022272021/1130577)

[AudioJack](https://www.digikey.com/en/products/detail/cui-inc/SJ1-3513N/CP1-3513N-ND/738686)

[BSS138](https://www.digikey.com/en/products/detail/onsemi/BSS138/244210)

[XIAO ESP32-S3](https://www.amazon.com/ESP32S3-2-4GHz-Dual-core-Supported-Efficiency-Interface/dp/B0DJ6NQFKX/ref=pd_rhf_dp_s_ci_mcx_mr__d_sccl_1_1/137-7709202-3397348)

[PCF8574P Output Extender](https://www.amazon.com/Bridgold-PCF8574P-PCF8574AP-Extender%EF%BC%8C2-5V-6V%EF%BC%8CDIP-16/dp/B0GF1Q1GNG/ref=sr_1_3?s=industrial&sr=1-3)

[LCD 1602 screen](https://www.amazon.com/Hosyond-Display-Module-Arduino-Raspberry/dp/B0BWTFN9WF/ref=pd_rhf_dp_s_ci_mcx_mr__d_sccl_1_3/137-7709202-3397348)

### Recording Links

- https://lookout.hackclub.com/api/media/14632576-c89b-496d-beb1-f40932a76a6a/video.mp4

## Entry 20
- ID: 8077
- Author: Brandon
- Created At: 2026-05-20T03:04:15Z

### Content

When shopping for the components for the Walkman PCB, I tried to use JCLPCBs feature where I would upload a BOM of my project and they would automatically pull up all the components that I would need all on the JCLPCB website, so that I could order them all without having to manually search for them.
Reality isn't that simple, however, because when I searched up the XIAO ESP32 S3 (my MCU), JCLPCB showed that I could only order it when I used their "PCBA" service, which means that I could HAVE to pay them to assemble it, not just deliver the components separately with the PCB, which would end up costing me more money, which isn't desirable.
![Screenshot 2026-05-19 214245.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTc2NDksInB1ciI6ImJsb2JfaWQifX0=--64fde1b3690468bcf74b27b0a3168050c6fcd771/Screenshot 2026-05-19 214245.png)
After finding links online that I could use to purchase all the components, the only troublesome one to find was the MAX98357A Amplifier.  For the MAX98357A, I couldn't find a breakout board footprint for my PCB Editor, and the only footprint that I was able to find is the smaller version (the Quad Flat No-Lead package), which only has flat metal parts that need to be soldered onto the PCB directly, and it doesn't have pins to guide soldering.  This meant that soldering this component would be very difficult, as a small mistake could end up in the whole amplifier not working properly.
![Screenshot 2026-05-19 215015.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTc2NTAsInB1ciI6ImJsb2JfaWQifX0=--4ceef34914bd075866b961e3c0ddb453b139bad9/Screenshot 2026-05-19 215015.png)
![Screenshot 2026-05-19 223823.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTc2NTEsInB1ciI6ImJsb2JfaWQifX0=--71ac990732a02bab7f05a20a8929296cc18399f3/Screenshot 2026-05-19 223823.png)
I'll ask my engineering teacher for help on this, and maybe some of my peers if they can provide some replacements for this amplifier.


### Recording Links

- https://lookout.hackclub.com/api/media/77460058-c71a-43a5-8f47-4bcd787b8f62/video.mp4

## Entry 21
- ID: 8572
- Author: Brandon
- Created At: 2026-05-23T02:49:57Z

### Content

With the soldering eminent, I decided to research more about if I could solder all the components using just a regular soldering kit, like a Pinecil or something.  Turns out that for most of the components, yes, because I had made sure that most of them use THT (Through-Hole) pins, and therefore allowed a lot of room for error. 
![Screenshot 2026-05-22 203221.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTg3NTgsInB1ciI6ImJsb2JfaWQifX0=--d7eaff558e15290f979ee25ebc16c803072ff364/Screenshot 2026-05-22 203221.png)
 However, I had some "Surface Mount" components, namely the PCM5102 and the microSD card slot.  And to add to that, there were the BSS138 components that had to be surface mounted also: luckily, I found a footprint for the BSS components that allowed for a larger error margin.
Here's the comparison of when I changed the footprint for the BSS (I changed the the larger footprint for it):
![Screenshot 2026-05-22 202326.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTg3NjAsInB1ciI6ImJsb2JfaWQifX0=--8fd8d587e3f8d951ce67e53dec39323ce1e88746/Screenshot 2026-05-22 202326.png)
I didn't realize that I forgot to press F8 to update my PCB Editor for the resistor ladder, so when I updated it to bring in my large BSS footprints, I was surprised to get a whole slew of DRC errors about some "short circuiting"?  Turns out with my current track and wire configuration, I was connecting a lot of GPIO pins directly to power pins (e.g. 3V3 pins).  I also saw some blue "requirement" lines that confused me, as they were already connected:
![Screenshot 2026-05-22 210057.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTg3NjEsInB1ciI6ImJsb2JfaWQifX0=--472b95dca88c9f661d7d8ce9ef17b193f12b4ec3/Screenshot 2026-05-22 210057.png)
After I deleted the extraneous connections, through, I was able to correct the tracks and wiring.
I also ended up deleting the Connector 01x02 component from the PCB, after using a past (guided) PCB project that had battery wires go through a punched hole in the PCB to have its wires itself become pins for soldering (it's an audio recorder):
![IMG_7832.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTg3NjMsInB1ciI6ImJsb2JfaWQifX0=--7b094b6373fa2bf99ace3d16bb2c2a5a33d3d8c4/IMG_7832.jpg)
Getting some help with Claude, I deleted the component, and wired a new component called "Jumper" directly to the GND and the power pin.
![Screenshot 2026-05-22 212337.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTg3NjQsInB1ciI6ImJsb2JfaWQifX0=--9bf9a079254cf40f6449a9252be01a0409eca945/Screenshot 2026-05-22 212337.png)
Looks much cleaner! (also saves me some money)

### Recording Links

- https://lookout.hackclub.com/api/media/549c812f-7b8f-4877-ad81-e96325f5bbf0/video.mp4

## Entry 22
- ID: 8780
- Author: Brandon
- Created At: 2026-05-24T03:22:38Z

### Content

I decided that Surface-Mounting Soldering was definitely not for me, and after having found the larger footprint for the BSS components, I wasn't about to go smaller than those footprints for any other component, and that included the PCM5102A component that I was using for audio conversion.  The raw component itself looks like it has less than 1mm of tolerance when soldering it, so instead of trying to suck it up and try to solder the microscopic pads for myself or resorting to having JCLPCB solder it for me (PCBA), I turned to another solution: Amazon!
I was planning to buy a board from [this link](https://www.amazon.com/PCM5102-PCM5102A-Digital-Converter-Raspberry/dp/B0DNW32Y46/ref=sims_dp_d_dex_ai_rank_model_1_d_v1_d_sccl_1_3/137-7709202-3397348?psc=1), it seems like a good deal.  Another thing: the module includes an AudioJack as well!
Well, it perplexing at first to figure out which of my previous pins should go to relative to the module, because originally I had imported the PCM5102 and the AudioJack symbols separately onto the Schematic and manually wired them together as per their datasheets, but now all I had was this to work with as a "datasheet".
![Screenshot 2026-05-23 221242.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTkzMTQsInB1ciI6ImJsb2JfaWQifX0=--9436d66cb1e1ddc7f1f92ac27905279445f393de/Screenshot 2026-05-23 221242.png)
Given that I found this module on Amazon instead of a electronics vendor, I found no footprint files or anything, so I had to make my own custom symbol (in which I forgot to give each pin a number, which I'll have to fix in next session).
![Screenshot 2026-05-23 222311.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTkzMTUsInB1ciI6ImJsb2JfaWQifX0=--3f56e75cdeb7d8a68577671675304d30401a0e2c/Screenshot 2026-05-23 222311.png)
I made a footprint for it also, but considering that it's a module, I just slapped on a Connector 01x15 on my PCB Editor.  It's pretty longggggg.
![Screenshot 2026-05-23 222346.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTkzMTYsInB1ciI6ImJsb2JfaWQifX0=--ccb706ddb69312350d8d5931c4a4574f8ac9bb9c/Screenshot 2026-05-23 222346.png)
Most of my time as allocated to reorganizing the tracks and wires on the PCB Editor, but seeing as to how messy the editor became after my shift to the module, which entailed the deletion of a whole lot of resistors and capacitors, as well as the deletion of the AudioJack and the PCM5102A themselves, I couldn't simply just rewire: I had to do some "track and wire demolition" to clean it all up.  Here's a before and after of the edits I made today: the track and wire clean ups will continue next session.
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTkzMzUsInB1ciI6ImJsb2JfaWQifX0=--b4b2adae247f92de758037b16b363b20001b5a84/image.png)


### Recording Links

- https://lookout.hackclub.com/api/media/dcd21fd8-4de7-4ac4-a70e-f2e3dfff6cf8/video.mp4

## Entry 23
- ID: 9026
- Author: Brandon
- Created At: 2026-05-25T03:55:23Z

### Content

With my Amazon delivery coming in for my LED project components, I also got some components in for the Walkman project, such as the PCM5102A x Audio Jack module
![IMG_7858.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTk5NzksInB1ciI6ImJsb2JfaWQifX0=--54ada44f7a6bc3ab648cc53e6badd924e1293f21/IMG_7858.jpg)
After fixing the custom symbol for the PCM5102A x the Audio Jack and rearranging the components to make the PCB smaller, I got to work for wiring the new PCB version that I had for the Walkman.
After grinding for a bit, I got a zero-error DRC check :)
![Screenshot 2026-05-24 233313.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTk5NzUsInB1ciI6ImJsb2JfaWQifX0=--ea556b95cf438372b069e0b2c543858f7c45bdc7/Screenshot 2026-05-24 233313.png)
![Screenshot 2026-05-24 233411.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTk5NzYsInB1ciI6ImJsb2JfaWQifX0=--2b643010c6113e97f941d4b33b331029f7831cf6/Screenshot 2026-05-24 233411.png)

### Recording Links

- https://lookout.hackclub.com/api/media/3eefe05a-84d3-42b4-9a87-87320b506ef0/video.mp4

## Entry 24
- ID: 9152
- Author: Brandon
- Created At: 2026-05-25T17:14:33Z

### Content

Here's a comparison between the two iterations of my Walkman PCB thus far:
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjAyNjYsInB1ciI6ImJsb2JfaWQifX0=--b7d0bc7b9e0d7cb87887a68f606dfaef82c67fdf/image.png)
Even though the dimensions aren't much smaller, at least I have no vias now :)
With the physical PCM5102 x Audio Jack with me, I measured out the dimensions of it (roughly 18 mm x 32 mm), so that I could make a little socket for it on my PCB in the OnShape rendering.
![image_5.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjAyNjcsInB1ciI6ImJsb2JfaWQifX0=--c53e691954333ef7d476010dd56e895676bd845a/image_5.jpg)
Exporting the newer version of the Walkman PCB, I CADed until my mouse broke (hyperbole), and drew all over my OnShape document into oblivion: after this session, I began printing the custom standoffs that I had created to verify their stability (as in making sure that they weren't too microscopic to work with).
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjAyNjMsInB1ciI6ImJsb2JfaWQifX0=--8bad26a93ee93cb75e68273e10d3b78535a0f73e/image.png)

### Recording Links

- https://lookout.hackclub.com/api/media/c1323cd9-1d13-40a9-ad3b-ee44cf9a60c6/video.mp4

## Entry 25
- ID: 9505
- Author: Brandon
- Created At: 2026-05-27T01:29:09Z

### Content

From yesterday's CADing session, I managed to print the custom standoff/case for the PCM5102A + AudioJack module (the printing time was NOT INCLUDED IN THIS SESSION'S TIME), and it fits pretty well!
![IMG_7877.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjExMjgsInB1ciI6ImJsb2JfaWQifX0=--32aa690fbf04419bacf536d89398f1d5cd6c6b7a/IMG_7877.jpg)
Moving on, I started to CAD the Walkman case, but as I made progress in make it (starting from the bottom of the PCB board), I noticed that my fingers most likely won't be able to go through the case in order to press the buttons (SW_PUSH buttons, in order to pause, play, skip, etc).  Even if I were to make an indent big enough to fit my fingers, the case will be very awkward to install, not to mention very open and have the PCB left open to the elements (i.e. rain).
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjExMzUsInB1ciI6ImJsb2JfaWQifX0=--ef579e96876b1266cd7573404ef9b6de65454726/image.png)
This was when I decided to finally search for a right-angle switch: I wasn't looking for one earlier because I assumed that they didn't exist.  I was browsing through KiCad's built-in switch footprints, and none of them seemed to work (most of the footprints didn't have valid 3D models to be shown on the 3D Viewer T-T) However, to my luck, there are quite a few "upright" switches out there on the internet, and I even found a Right-Angle Tactile Button" on the LCSC database!  Using easyeda2kicad via Powershell, I imported the "TC-S3601-3.5-260G-F0.6" into my Walkman project, assigned it to the 5 SW_Push switches that I had, and then rendered them on the 3D Editor: it looks pretty good! (Unfortunately the switches are SMD/surface-mounted, hopefully I can do that)
Coming up next, I'll have to rewire the PCB (yet) again, and render the new3D  version of the PCB in Onshape to make a case for it.


### Recording Links

- https://lookout.hackclub.com/api/media/d53d0c67-e778-4433-8d94-ddbf1983cd47/video.mp4

## Entry 26
- ID: 9509
- Author: Brandon
- Created At: 2026-05-27T01:54:52Z

### Content

![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjExNDcsInB1ciI6ImJsb2JfaWQifX0=--0eba10335cdf3436b7cab264674c58ee367ced34/image.png)
This time, rewiring everything for the new switches wasn't too hard, except this one GPIO1 pin connection, which required me to track a F. Copper (because the switches are SMD/Surface-Mount) all around the bottom of the PCB in order to not use a via (after all, I don't want to only use 1, that'll feel terrible, might as well use no vias).

### Recording Links

- https://lookout.hackclub.com/api/media/98271124-ea61-4c9b-931a-f127619c8ffc/video.mp4

## Entry 27
- ID: 9699
- Author: Brandon
- Created At: 2026-05-27T17:10:28Z

### Content

The other night, I was vacillating about wanting to buy the right-angle switches from LCSC immediately due to me being unsure if I had any other components out of all my PCB projects that I need to buy from LCSC.  Wanting to review my purchases, I updated my PCB BOM Google Doc to track all of my purchases and expenses.
Moving on; when I tried exporting my Walkman PCB, the right-angle switches came out wrong, **despite looking correct in the 3D Viewer**!  My first suspicion was that something was awry in the DRC (I forgot to check the DRC after switching to right-angle switches, actually :| ), and lo and behold, there was something wrong (albeit it wasn't the cause of the broken 3D model):
![Screenshot 2026-05-27 113622.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjE1MjQsInB1ciI6ImJsb2JfaWQifX0=--8ceb3dfeb8463e61e225a7a3eacfadb4955b1a07/Screenshot 2026-05-27 113622.png)
After repeated research, I initially thought that the DRC errors were stemming form how the 1 and 2 pin pads were too close to the two through-holes, so I tried scaling them smaller and moving the pads farther away from the holes, but all those methods didn't alleviate the problem.  After further research, I discovered that the through holes themselves were the problem, because they were the **wrong type of through-holes**!  They were **copper** through-holes instead of being **mechanical** through-holes, and the latter type was the correct one due to the holes only being necessary to provide a slot into which the switch can slide into (it has two pegs on the bottom that line up with said holes).
![Screenshot 2026-05-27 120203.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjE1MjksInB1ciI6ImJsb2JfaWQifX0=--7b2dca024015143f03a29eb42b0ca3ba367f29ab/Screenshot 2026-05-27 120203.png)
After changing the parent footprint of the right-angle switch to have the correct type of through-holes, I updated the rest of the switches to be correct, and thus the DRC errors disappeared!  (idc about stupid silkscreen Warnings, shut up KiCad)
![Screenshot 2026-05-27 120518.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjE1MzAsInB1ciI6ImJsb2JfaWQifX0=--c95809c9fea26211d92b860ed20589dffaef4805/Screenshot 2026-05-27 120518.png)
As I had mentioned before, though, these DRC errors weren't the cause of the misalignment seen in the 3D export of my PCB (.step):
![Screenshot 2026-05-27 120701.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjE1MzEsInB1ciI6ImJsb2JfaWQifX0=--44818912d057428e41b989dacad286e609740033/Screenshot 2026-05-27 120701.png)
The errors persisted even in the .stl version of the 3D export:
![Screenshot 2026-05-27 121824.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjE1MzIsInB1ciI6ImJsb2JfaWQifX0=--b2b436acb7cc5caff1fa1f891b44d4e57a402988/Screenshot 2026-05-27 121824.png)
Soon, I later learned that the 3D rendering that I was seeing in KiCad was actually a DIFFERENT file than what the .step and the .stl files were using to render the right-angle switches!  The rendering on KiCad **3D Viewer** was using the .wrl (a Blender filetype) version of the switch 3D file, while the export was using a .step filetype for all the components, and the .step file was secretly misaligned according to the PCB coordinates: I just didn't notice it because all I was seeing was the .wrl version of the switch, which was all correct.
When swapping the 3D Viewer in KiCad to use the .step file instead, the misalignment became apparent:
![Screenshot 2026-05-27 122201.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjE1MzQsInB1ciI6ImJsb2JfaWQifX0=--1e90691c1990e19114345472a5adbdc01b0ec46c/Screenshot 2026-05-27 122201.png)
After fixing this file mismatch, I finally got a correct export of the PCB in the form of a .step file (.step files are so cool, better than .stl for sure)
![Screenshot 2026-05-27 123423.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjE1MzUsInB1ciI6ImJsb2JfaWQifX0=--fad154f8aeffd60eb6193992f1dd45c5dcb6b155/Screenshot 2026-05-27 123423.png)

### Recording Links

- https://lookout.hackclub.com/api/media/6f7e2ba0-582d-431a-b0f8-310f3dec8b4d/video.mp4

## Entry 28
- ID: 9972
- Author: Brandon
- Created At: 2026-05-28T18:17:04Z

### Content

As I started making the case for the Walkman, yet again, I had questioned my PCB's design: this time, it wasn't about the five SW_PUSH buttons that I replaced, but was struck by a doubt: even though I used a battery cage of two AA batteries to power a PCB before (it was an audio recorder, pretty simple), would it power this PCB the same?  Yesterday, I did some research about a new PCB project that I was planning, and the power consumption for it was relatively more compared to my other PCB projects (including this one), and one main component that all the AI model assistants that I used for research all implored me to use some ["TP4056"](https://www.amazon.com/MakerFocus-Charging-Discharging-Interface-Protection/dp/B0CWNXKR4X), which is supposed to regulate the power between a battery and the XIAO and the rest of the PCB.  I didn't use something like this in my past PCB project!
Advice told me to use a LiPo battery, short for "Lithium Polymer", instead of a simple set of Alkaline batteries.  Makes sense in hindsight, however, because I want to be able to recharge my Walkman.
Alas, after much research and crashing out in front of Claude, Gemini, and other AI models for advice, I found myself surfing the web to look for answer on how to properly use a LiPo) battery, here's all the videos I looked at: some were confusing, others were quite helpful.
https://youtu.be/V_mZsiZcy7s
https://youtu.be/gmx536ov7i8 (wrong context because this is for much higher power demand, off-road RC cars)
https://youtu.be/o0TiboxnwWA
https://youtu.be/doyDc18SwfE
I also used this screenshot a lot when trying to explain that I was using a XIAO ESP32S3 that has a USB-**C** port, but a USB-**A** port.
![Screenshot 2026-05-28 115512.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjIzNzQsInB1ciI6ImJsb2JfaWQifX0=--6e820fd5296ab477aa7d00a64bd30d1a50123a0c/Screenshot 2026-05-28 115512.png)
After two long hours or doubt and searching, I discovered that there were two hidden pins on the backside of the XIAO ESP32S3, which were BAT+ BAT- for the LiPo battery to use.  This led me to make a design decision to raise the XIAO by a few millimeters to make room in which the wires for the battery wires can snake though to attach to the backside of the XIAO.
![Screenshot 2026-05-28 120619.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjIzNzUsInB1ciI6ImJsb2JfaWQifX0=--0404eedf3610965de47e3dc19c7c5fff2c7a58e3/Screenshot 2026-05-28 120619.png)
The lone connector represents the BAT+ pin, which will connect to the BAT+ pin/pad on the XIAO.
![Screenshot 2026-05-28 122826.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjIzNzYsInB1ciI6ImJsb2JfaWQifX0=--097176d0df2a2d4666c140e0f9c4d7e77c4b161b/Screenshot 2026-05-28 122826.png)


### Recording Links

- https://lookout.hackclub.com/api/media/ba6058f5-c3dd-450f-8589-5e6819ad06fb/video.mp4

## Entry 29
- ID: 10186
- Author: Brandon
- Created At: 2026-05-29T17:32:34Z

### Content

Today's progress can be summed up in six words: "one step back, one step forward".
I was in New York visiting family, when I realized that I had forgotten to push my KiCad changes to my GitHub repo from home, and the last time I did was was like a couple of weeks ago (dang it!) so I had to call my brother who was still home, where my desktop was in order for him to push the changes for me (he knows my computer password now...).
My brother also decided to name the commit name "larp" cause that's his favorite word nowadays, what a silly guy.
I also had to update some of the footprints and symbols and 3D models because even though they were saved on my desktop computer, they weren't saved on my laptop computer that I had to use, and they weren't in the GitHub as well.  Luckily, I have my BOM on Google Docs, so I could use the easyeda2kicad cmd tool to bring over the necessary symbols, footprints, and 3D models.  
Using easyeda2kicad on my laptop was a bit trickier, because I didn't notice that my file paths were going under the pesky OneDrive/ folder.  This took me about 20 minutes to realize :(
![Screenshot 2026-05-29 125104.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjMwMzEsInB1ciI6ImJsb2JfaWQifX0=--e73db371793f819ea20211d14a5d4f3e7740a599/Screenshot 2026-05-29 125104.png)
![Screenshot 2026-05-29 125118.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjMwMzIsInB1ciI6ImJsb2JfaWQifX0=--fa8d621aa85caa53ab6b18b550695bf65275a586/Screenshot 2026-05-29 125118.png)
Also, the 3D models on the PCB editor for the right-angle switches weren't appearing, and supposedly there were two references to the 3D models and footprints for the component: one set in the "Global Libraries" tab, and the other in the " Project Specific Libraries" tab, which somehow caused a problem.  When I deleted the latter version of the easyeda2kicad library, everything looked as normal, and better yet, I didn't have to adjust the offsets for the 3D offsets for the 3D Viewer!
![Screenshot 2026-05-29 130241.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjMwMzMsInB1ciI6ImJsb2JfaWQifX0=--47e33f7eecb6d5f1f5a78ee93a749d55eb359271/Screenshot 2026-05-29 130241.png)
![Screenshot 2026-05-29 130247.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjMwMzQsInB1ciI6ImJsb2JfaWQifX0=--7b293dd930ecfd935e46996455780995a26d3903/Screenshot 2026-05-29 130247.png)


### Recording Links

- https://lookout.hackclub.com/api/media/6cab809b-ef46-4a02-9cd1-0794b84988e9/video.mp4

## Entry 30
- ID: 11538
- Author: Brandon
- Created At: 2026-06-04T04:29:34Z

### Content

With me deciding that the XIAO ESP32S3 needing to be off the surface of the PCB, I looked at [the connectors that I was going to buy](https://www.amazon.com/Glarks-Connector-Assortment-Stackable-Breakaway/dp/B07CWSXY7P) to ensure that the LCD and the XIAO would have connectors at the same height in the 3D rendering (after all, I'm only getting one set/kit of connectors/pin headers).  I deduced that the total height between the components and the PCB should be 10mm (8mm + 2mm) for both the XIAO and the LCD screen.
![Screenshot 2026-06-03 154534.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjY3OTIsInB1ciI6ImJsb2JfaWQifX0=--490d0988c1548e72c474166c5ef545f1f0c7272c/Screenshot 2026-06-03 154534.png)
Fixing the distance (i.e. Z-offset) for the XIAO, I realized that the connectors in the LCD 3D model rendering didn't match the connectors that I was going to buy from Amazon, so I had to edit the LCD's offset as well, even though the connectors would look like they're clipping through the PCB in the 3D model (while in reality, they wont).
![Screenshot 2026-06-03 162126.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjY3OTQsInB1ciI6ImJsb2JfaWQifX0=--61b43a693d708cf8ab902b34ef799ea37af89256/Screenshot 2026-06-03 162126.png)
Now they're level with each other!
![Screenshot 2026-06-03 155829.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjY3OTMsInB1ciI6ImJsb2JfaWQifX0=--65a659af320128b616c933470a687357074df53c/Screenshot 2026-06-03 155829.png)
I also noticed that the pin header that I was using for my LiPo battery from the back of the PCB seems to be smaller than the rest of the pins, and it was because it was using a 1mm x 1mm pin header instead of the standard 2.54mm x 2.54mm, and after changing that in the Footprint Editor (I couldn't change it in the PCB Editor > Properties), I finally exported the .step 3D file for the PCB into OnShape.
![IMG_8037.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjY3OTEsInB1ciI6ImJsb2JfaWQifX0=--a6c878f052eb1473c972d0e5913f5db09320dfcb/IMG_8037.png)
After this, I went on my phone for a bit to order some of the Walkman components from DigiKey to get that task knocked out.  (They don't have International Direct Shipping or whatever it is, the cheapest delivery they have is USPS Ground T-T)
This session was done entirely on my (crappy) laptop, which is why I wasn't as productive as I could've been during this session)

### Recording Links

- https://lookout.hackclub.com/api/media/7f407e9f-4e37-4dce-be4b-ff870c2f9db4/video.mp4

## Entry 31
- ID: 14262
- Author: Brandon
- Created At: 2026-06-15T15:55:51Z

### Content

When I got my order from DigiKey, I realized that my Omron SW SPST switches were wrong for my power on/off case!  After looking at a friend's KiCad project, I copied his schematic and usage for a power switch (i.e. a SW DPST instead of a SW SPST).
![Screenshot 2026-06-13 111224.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzI4MzAsInB1ciI6ImJsb2JfaWQifX0=--e4510902c0417c008ba410b71ea1bfa1aaee1f46/Screenshot 2026-06-13 111224.png)
After getting back from a trip from Colorado, I managed to talk to one of my more PCB-savvy friends online and discussed past projects that he had done with XIAO's. Through these conversions, I learned how he implemented batteries and power management within his PCB projects, in some ways more sketchier than others.  For example, he told me that when soldering jumper wire holes (punched holes) to the battery pads on his XIAO, he only used the solder, making a "melted solder trail" from the jumper wire holes to the pads, which, as he admitted, was indeed sketchy.  We were discussing how to connect the BAT+ and BAT- (i.e. the battery pads) on my XIAO to my SW_SPDT power switch and the LiPo battery that my friend suggested.  What I had initially was using a pin connector to plug into a JST connector onto the PCB, and then to have another wire connect that pin connector to the battery pads through direct SMD soldering: better than making a melted solder trail, but still sketchy.  That's when my friend proposed that I directly make the battery pads on the back of the XIAO come into contact with the PCB.  That's when I remembered that it is indeed possible to have a footprint on a PCB just be a simple surface/SMD pad of exposed copper to solder onto, so I did just that.  Using the footprint editor on the official KiCad document from Seeed Studio (the group that made the XIAO series), I identified the dimensions of the pads, and the distances they were from the tip of the USB-C outlet.  
![Screenshot 2026-06-13 142634.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzI4MTIsInB1ciI6ImJsb2JfaWQifX0=--7ede5dc42a77b9ed0b3c01491b95fec8bf861da1/Screenshot 2026-06-13 142634.png)
![Screenshot 2026-06-13 143205.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzI4MTMsInB1ciI6ImJsb2JfaWQifX0=--e8f9c4bc42e9ae75c07691e0d89b9e9d8576d1ef/Screenshot 2026-06-13 143205.png)
![IMG_8179.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzI4MTQsInB1ciI6ImJsb2JfaWQifX0=--da7a27db55a7306eed200a087c25e0ae5a3920ac/IMG_8179.jpg)
![Screenshot 2026-06-13 150057.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzI4MTUsInB1ciI6ImJsb2JfaWQifX0=--f6f05a619530c2fee0925f192663cd8435541b33/Screenshot 2026-06-13 150057.png)
![Screenshot 2026-06-13 151325.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzI4MTYsInB1ciI6ImJsb2JfaWQifX0=--64ccf7b54acfb0651be936dc190aa52d990cce09/Screenshot 2026-06-13 151325.png)
After checking my work using the 3D Viewer, it turns out that my dimensioning was pretty accurate!
![Screenshot 2026-06-13 153420.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzI4MjQsInB1ciI6ImJsb2JfaWQifX0=--528f6ff561592ff322d6f0363e14036d8d569d7f/Screenshot 2026-06-13 153420.png)
Also, I spent a lot of time after the XIAO power distribution change to rewire everything on my PCB to make it more compact, where I had to use 9 vias, because I decided that a smaller size was worth the addition of vias in my PCB design.

### Recording Links

- https://lookout.hackclub.com/api/media/786ff3d8-b553-4803-a038-e6dd8a68ad80/video.mp4

## Entry 32
- ID: 14669
- Author: Brandon
- Created At: 2026-06-17T02:00:24Z

### Content

Upon receiving the LCD1602 from Amazon, I took a look at it:
![IMG_8189.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzM5OTQsInB1ciI6ImJsb2JfaWQifX0=--309b81dbab041bd960dde364c3d167a1d1553e3c/IMG_8189.jpg)
![IMG_8190.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzM5OTMsInB1ciI6ImJsb2JfaWQifX0=--710659bed673a92e6b55b1f1cb7a99e77e6aa9f4/IMG_8190.jpg)
I noticed that there was an auxiliary board attached to it: what would it be?  I started to look back on the [Amazon link]() which I got the LCD from, and sure enough, it said that it came with a PCF8574, which worried me because I wasn't sure if I was using the PCF.  After a look at my BOM, however, I actually do indeed use the PCF8574, and since it's already attached to the LCD out of the package, I didn't have to worry about the PCF taking any more space on the PCB!  Therefore, I went ahead and deleted it from the schematic and the PCB editor.
This also meant that I had to create a custom symbol and footprint for the PCF x LCD combo, and after fumbling through the measurements for the components' pins, I got it on the PCB editor.
![Screenshot 2026-06-15 125114.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzM5OTIsInB1ciI6ImJsb2JfaWQifX0=--8bd3e44c226bb86ea063bcd8148f5a3314868c35/Screenshot 2026-06-15 125114.png)
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzQwMDMsInB1ciI6ImJsb2JfaWQifX0=--80736cfe85ff714e272a41c1ebd9c7f82b81658b/image.png)
Note that the right-angle pin connectors will make it impossible for me to install the LCD onto my PCB board as intended, as the LCD would now be sticking up and out of the board instead of being flat against the PCB board's surface.  Thus, I'm in the process of (carefully) bending the right-angle connectors straight.  Due to the potentiometer for tuning the LCD's brightness is also on the backside of the LCD, I'll have to use a provided JST connector (that came with the component) to test the brightness before fully installing it (i.e. soldering it) onto the PCB, which will be my Walkman.
![IMG_8191.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzQwMTQsInB1ciI6ImJsb2JfaWQifX0=--7f5f837ca6e65af66c82673691775a6123817476/IMG_8191.jpg)
This isn't a final version of the PCB board, however, as I still have more wiring to do, as well as add the PCM5102 x AudioJack combo onto the PCB editor as its own footprint, because I changed my mind about keeping it as a row of Pin Connectors, and I want to give it its own footprint as I had given the PCF x LCD combo.


### Recording Links

- https://lookout.hackclub.com/api/media/8bb49337-191b-4874-89d2-8837a6cf05f2/video.mp4

## Entry 33
- ID: 14899
- Author: Brandon
- Created At: 2026-06-18T01:25:20Z

### Content

Before I went ahead and made the footprint for the PCM + AudioJack component, this is where I had left off since last session.  With the plentitude of lines streaming across the editor, it was foreshadowing as to how long this session would take in order to wire the components all back together.
![Screenshot 2026-06-15 140439.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzQxMDAsInB1ciI6ImJsb2JfaWQifX0=--6de1300003b2a4e6ee02edcb383c33444bfdf499/Screenshot 2026-06-15 140439.png)
This is when I started customizing the footprint for the component:
![Screenshot 2026-06-15 141042.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzQxMDYsInB1ciI6ImJsb2JfaWQifX0=--e443435dad3828a26a25cc69d8ee07c5cae8c9f4/Screenshot 2026-06-15 141042.png)
![Screenshot 2026-06-15 141359.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzQxMDcsInB1ciI6ImJsb2JfaWQifX0=--6fc63536fac8f34693f09e8214fd3ff4efa959c4/Screenshot 2026-06-15 141359.png)
Finally, it took be about a couple hours and a lot of deep breathing (it wasn't that hard...) to finally be rewarded with a 0-error DRC report :D
![Screenshot 2026-06-15 165358.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzQxMDgsInB1ciI6ImJsb2JfaWQifX0=--e6592fc0892bd1afc29cd3e1f51801630aec7d99/Screenshot 2026-06-15 165358.png)
My usage of vias was still a lot by my standards, albeit minimal, around 8-15.


### Recording Links

- https://lookout.hackclub.com/api/media/5cc80606-33cc-4b6f-b236-0f9903fcf221/video.mp4

## Entry 34
- ID: 15139
- Author: Brandon
- Created At: 2026-06-19T03:16:50Z

### Content

This session, I first discovered that the LCD + PCF component footprint I made was wrong!  Using my DigiKey ruler yet again, I measured out the lengths of all the pin dimensions from the edge of the LCD board, and tediously inputted all their measurements onto the footprint.  So, this also meant that I had to change the routing on the PCB Editor.  
This is a picture of my verifying the new dimensions and placements of the pins for the LCD + PCF component.
![IMG_8198.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzUzMDIsInB1ciI6ImJsb2JfaWQifX0=--2a32d41af457746263782cc00064c1cb6bfbf1e4/IMG_8198.jpg)
Then, I noticed that there was a "5V" pin on the LCD + PCF component that was empty (i.e. not routed to anything) and mislabeled (it was supposed to be the VCC, which would be the XIAO's VBUS pin).  I decided that it was time to update my schematic and fix all the wrong and missing wirings, if any.  I later learned that the 5V/VCC pin on the LCD + PCF component should've been connected to the VBUS pin from the XIAO, and after further inspection of the "bidirectional I2C level shifter", aka the BSS138, I realized that I wired it wrong in the schematic.
I know this because of a reference image I found online, showing the correct way to wire a BSS between to levels (in my case, the lower-level "LV" would be the 3.3V from the XIAO's side, while the higher-level "HV" would be the 5V from the VBUS and LCD + PCF's side).
![Screenshot 2026-06-17 141005.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzUzNzUsInB1ciI6ImJsb2JfaWQifX0=--1d8be950bef5e6f84723465482a1e25c722acef6/Screenshot 2026-06-17 141005.png)
I used labels differently to help me understand what was going on in the schematic.
![Screenshot 2026-06-17 140620.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzUyMDksInB1ciI6ImJsb2JfaWQifX0=--90f7b7600b7a85194a3a04d44c2d1f279f2cc83f/Screenshot 2026-06-17 140620.png)
On the right side of this image you'll see the custom symbol I made for the LCD + PCF component.
![Screenshot 2026-06-17 140930.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzUyMTAsInB1ciI6ImJsb2JfaWQifX0=--6e893bf88d66bcffaf1fc2c5706b6ecfee67a93b/Screenshot 2026-06-17 140930.png)
With the new schematic, I returned to the PCB Editor, pressed F8 to update it, and got back to wiring.
![Screenshot 2026-06-17 141431.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzUyOTgsInB1ciI6ImJsb2JfaWQifX0=--d6f2bfcb33a4a21ddde83d6445a869a1680b3978/Screenshot 2026-06-17 141431.png)
![Screenshot 2026-06-17 142124.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzUyOTksInB1ciI6ImJsb2JfaWQifX0=--45caddac2af62b6f29c7dbf95d82b938739903c3/Screenshot 2026-06-17 142124.png)
Once again, the amazing Brandon wires everything together with no DRC errors on the first try!
![Screenshot 2026-06-17 143231.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzUzMDAsInB1ciI6ImJsb2JfaWQifX0=--f047f0a025b319f66b5ad24382404accb14c485a/Screenshot 2026-06-17 143231.png)

### Recording Links

- https://lookout.hackclub.com/api/media/62045419-c02e-4d07-a1a9-3880c5e7c5d0/video.mp4

## Entry 35
- ID: 15405
- Author: Brandon
- Created At: 2026-06-20T01:01:07Z

### Content

If I wanted to make a 3D printed housing for my PCB (it better not be out and about exposed to the elements...), I had to either:
One: Find the 3D models of the custom components that I bought from Amazon online on the interwebs

**OR**
Two: Dimension the components myself a bajillion times to make sure that I have everything correct (I really didn't want to do this, for this leaves a lot of room for error, and I would rather not 3D print many different attempts of making a housing if the failed versions are just a couple millimeters off)
This [Amazon link](https://www.amazon.com/Hosyond-Display-Module-Arduino-Raspberry/dp/B0BWTFN9WF?ref_=ast_bl_cpl_dp) that I used to buy the LCD + PCF component didn't have a 3D model component linked to it, so I went looking elsewhere for an accurate 3D modelling for it.  Good news was, I found one on [Autodesk](https://www.autodesk.com/community/gallery/project/155964/lcd-1602-i2c), but the bad news was that the file was a f3d file format, a format exclusive to Fusion.  This meant that I had to find some way to convert it into a STEP or STL file in order to be about to use it in my PCB Editor for my LCD.
That said, I'll have to continue looking for the AudioJack + PCM component's 3D model some other time (or...I could dimension it myself; this component is not as bad because it's more "flatter" than the LCD)
After signing up for an Autodesk free trial account, I went though many tutorials online to help me get to the part where I could finally import my f3d file into a STL file, and when I imported it into OnShape, I turned it into a STEP file which I used to represent the LCD in the KiCad PCB 3D Viewer.
![Screenshot 2026-06-18 225502.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzYwMzAsInB1ciI6ImJsb2JfaWQifX0=--dda50abe50836549dbc83e84099d264ab89b40e1/Screenshot 2026-06-18 225502.png)
Many more iterations were done in terms of aligning the 3D model of the LCD to the mounting holes on the board, and then measuring the difference between the pins on the LCD vs on the board, and then going back tot he footprint editor for the LCD to change the positions of said pin holes.
![Screenshot 2026-06-18 230116.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzYwMzEsInB1ciI6ImJsb2JfaWQifX0=--4550c1068be8f769b70697b905a2308bab1c50f7/Screenshot 2026-06-18 230116.png)
I had to move the dimension of the LCD and pin holes for about three cycles until I got the positioning right (I think...I'll have to see when I actually 3D print this new version of the PCB to verify the correct dimensioning of the PCB's holes to the LCD's pins.
In KiCad, though, this looks correct.
![Screenshot 2026-06-18 231322.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzYwMzIsInB1ciI6ImJsb2JfaWQifX0=--80b0630e1c9bcca6d4749bb0272fa7ad74a6eaba/Screenshot 2026-06-18 231322.png)




### Recording Links

- https://lookout.hackclub.com/api/media/7ab3bcfd-ab04-411a-8d7f-de37684c221d/video.mp4

## Entry 36
- ID: 15952
- Author: Brandon
- Created At: 2026-06-21T04:03:14Z

### Content

On June 19, I finally got the XIAOs from China, which meant that I could finally verify dimensions of the BATT pads on the XIAOs and compare them to their estimated dimensions that I had on my XIAO KiCad footprint.
![IMG_8223.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzY3MDAsInB1ciI6ImJsb2JfaWQifX0=--cec37317abc9bc7ddec8bb928f6f76607f8327ce/IMG_8223.jpg)
Exporting the Walkman PCB as a STEP file, I made another test print for the PCB board that, when printed, will show me if the BATT pads dimensions and positions match with the real XIAO (that I'm holding in the picture).
![XIAO bat pad comparison.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzY3MDEsInB1ciI6ImJsb2JfaWQifX0=--a12046fe15e5b07408a34525b12acf39eca89534/XIAO bat pad comparison.jpg)
As for the LCD, I managed to verify its pins' positions on a previous PCB test print, as shown:
![IMG_8221.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzY3MDIsInB1ciI6ImJsb2JfaWQifX0=--7d9c11c5d9cf0bfbebfea3f9d5f4c749bbec9aff/IMG_8221.jpg)
One thing I realized about the LCD's orientation on the PCB, through, is that the display was shown to be upside-down according to the 3D model that I retrieved from a previous, recent session, so I had to rotate the LCD's footprint in the PCB Editor by 180 degrees and rewire its pins' tracks.
Moving on, I decided to measure the AudioJack + PCM component's dimensions using my DigiKey-branded ruler, and CADed its rough design and shape on OnShape, which I later exported as a STEP file and added to the PCB's 3D model on KiCad.
![IMG_8228.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzY3MDYsInB1ciI6ImJsb2JfaWQifX0=--d92d658ff7e6f8177d75be10f8cd52f6eaee0ee2/IMG_8228.jpg)
After adjusting its positions on the 3D Viewer to align with the X and Y of the footprint, I saw that the AudioJack (3.5mm, by the way) was colliding with the right-angle buttons.
![Screenshot 2026-06-19 201621.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzY3MDksInB1ciI6ImJsb2JfaWQifX0=--c0d32c3f0beb4c00cc3e4b9ea8d96f5f34d743ac/Screenshot 2026-06-19 201621.png)
Raising the component by 2.54mm (I'm going to use a pin connector for it on the real PCB to give it that extra elevation), the component wasn't colliding with the switches/buttons anymore.
![Screenshot 2026-06-19 201859.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzY3MTMsInB1ciI6ImJsb2JfaWQifX0=--d8418c6005044ceebc4b83dcae24c6482e1ef1b7/Screenshot 2026-06-19 201859.png)
![Screenshot 2026-06-19 201939.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MzY3MTIsInB1ciI6ImJsb2JfaWQifX0=--df4b612dd2b0e6bcbc94df581a9475bc47f40dbe/Screenshot 2026-06-19 201939.png)
Finally, I exported the PCB to import it onto OnShape to help me make the 3D printed housing for it.  Unfortunately, there were issues with exporting it as a STEP file, for the LCD would vanish in the file format, so I had to resort to using STL to export the PCB.  I hope that I don't have to restart making the housing because of yet another PCB addition this time...

### Recording Links

- https://lookout.hackclub.com/api/media/c2e94805-d0f2-42f8-bb2d-849d7580b000/video.mp4

## Entry 37
- ID: 16097
- Author: Brandon
- Created At: 2026-06-23T17:12:05Z

### Content

All that's left are some finishing touches to verify dimensions, and then I was going to plan to order the PCB.
Using OnShape to print some custom standoffs, I made sure that the pin locations for the LCD1602 and the standoffs would align to it.
![IMG_8249.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mzg4MTksInB1ciI6ImJsb2JfaWQifX0=--c64a62af9b0a70f7ef8bed2a0c2d44696bd2f276/IMG_8249.jpg)
Additionally, I also 3D printed a thin version of the PCB that had holes as to where the BATT pads on the XIAO were to ensure that the pads BATT pads on the PCB corresponded (touched each other) between the board and the XIAO itself.
![IMG_8248.jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mzg4MTEsInB1ciI6ImJsb2JfaWQifX0=--aaa06b6b9fddb28871bb37c0e1db00a78bbdbbc5/IMG_8248.jpg)
Finally, my Walkman PCB order is now sent to JLCPCB, waiting to be manufactured and shipped.
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mzg4MTQsInB1ciI6ImJsb2JfaWQifX0=--62ba6f1e5f1c956320ec633b2d49177b184f2f1d/image.png)

### Recording Links

- https://lookout.hackclub.com/api/media/ef89657a-93c7-48b7-af75-a8e273279bcc/video.mp4
