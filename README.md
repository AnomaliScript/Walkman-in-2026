# Walkman-in-2026
As a part of Hack Club's "Fallout" challenge, I attempt to build a replica of Makoto's walkman (from Persona 3) using KiCad, Onshape, and hopes and dreams.

This Walkman composes of many capacitors, resistors, an Audio Jack, a microSD card socket, LCD display, four buttons, an on/off switch, and most importantly, a XIAO-ESP3-S3 to make it all work!
Most, if not all of these components are THT, or "through-hole technology", meaning that the components have pins that go through holes in the PCB, making them easier to soldier, and that's why I chose THT components (with the exceptino of the microSD card reader), because I'm not a soldering expert (yet).

## V0.1
I made my own custom "standoffs" which are supports that support the LCD display, because it needs extra vertical room in order for its pins to be connected to the PCB.  I 3D printed both a "screw" and a "non-screw" version of the standoffs, to test which one would work best (standoffs are small, and the smaller a print is, the worse small details, like screw patterns, will be).

<img width="1584" height="619" alt="image" src="https://github.com/user-attachments/assets/02e7ecab-421a-4289-b0a8-4cb60dd4821a" />

The screw standoff's didn't work, becasue my 3D printer can't print with that amount of sub-millimeter precision, so I'll just have to use the "non-screw" version of the standoffs.

## V0.2
The biggest change from V0.1 was the addition of an Amazon-purchased breakout board that covered both the AudioJack (3.5mm diameter) and PCM5102A stereo.  After all, the PCM5102A is indeed a really tiny chip, and with the soldering iron that I was getting, it wasn't likely that I could've soldered the chip using SMD (surface mount) on my own.  Consequently, I had to rewire the whole PCB (this will happen many times...) to compensate for this change.
What I specifically did was delete the AudioJack and PCM components from the PCB, and put a 16-pin connetor row in its place to set it up for wires to connect to the breakout module (a decision I would later go back on).
I also cleaned up the BOM a little bit, but it still was missing a lot of components compared to the final one (which I will link in the bottom of this README).

<img width="696" height="477" alt="image" src="https://github.com/user-attachments/assets/70a0d6f5-14c3-460b-9228-4fb12f12b747" />

I was planning to get many of my components from my school's makerspace, however since Georgia school years end in mid-May, I lost access to those spaces, and therefore couldn't access those resources: this meant that I had to go shop online (i.e. Amazon and Digikey).
V0.2 was also when I finally started to consider how to power this whole contraption, and the conclusion I came up with was simply to add some punches holes (called  "Jumper" in the KiCad schematic) to have the battery wires solder through.

<img width="705" height="392" alt="image" src="https://github.com/user-attachments/assets/aee5ca89-15e2-4d3a-b473-65ba0e88fba8" />

<img width="923" height="475" alt="image" src="https://github.com/user-attachments/assets/4b481f30-f795-4408-9fff-38dae65b8a6f" />

## V0.3
The buttons on the Walkman PCB looks a bit off; maybe it's because they're not tilted 90 degrees!  While implementing right-angle switches, I learned about the different types of drill holes that KiCad offers (I had the wrong type of hole for the switches' footprints which was giving me DRC errors).

<img width="472" height="469" alt="image" src="https://github.com/user-attachments/assets/10d7de40-d570-4982-9803-ad306186ebac" />

This was also when I became very insecure about my power management system, so this was when I learned that the XIAO-ESP3-S3 in fact has a built-in nattery management system that rules out the need for Buck converters and other auxillary power managemtn components, which was a huge relief after having done power research for a couple of days straight.  The only problem was how to get the power tracks/wires to connect to the bottom of the XIAO, becasue that's where the XIAO's battery pads (BATT) are.  Seeing as to how laying the XIAO against teh PCB would make it impossible for a wire to reach under the XIAO, I decided to elevate it using connectors (not shown in the KiCad 3D Viewer below).

<img width="888" height="474" alt="image" src="https://github.com/user-attachments/assets/1eaf39fb-6490-43df-bae9-2569938b3b9d" />


## V0.4
I went back on my decision to physically elevate my XIAO from the PCB.
After a family vacation, my refreshed mind preferred to create pads on the XIAO footprint itself.  By adding the BATT pads onto the footprint itself, the XIAO, when it comes in contact with the PCB direcly, would have its BATT pads touch the PCB's corresponding pads, requiring no extraneous equiment to connect the two.
This customization of the orignal XIAO-ESP32-S3 footprint required me to refer to Seeed Studio's offical KiCad files in order to determine the dimensions and position of the BATT pads, becasue the XIAOs that I ordered were still in transit at the time, so I had no other reference.

<img width="576" height="474" alt="image" src="https://github.com/user-attachments/assets/86853d32-9630-4bf7-96e0-507ee271ec48" />

The XIAO BATT pads and its PCB footprint counterpart, in theory, seemed to perfectly align with each other.

<img width="485" height="472" alt="image" src="https://github.com/user-attachments/assets/997f2045-138b-43eb-9b9e-b4926167bb52" />

I also learned that I had ordered the wrong type of switch for the power, as I ordered a SW_SPST (a button) instead of a SW_DPST (an actual power switch that toggles), so I had to order SW_DPST switches.
The LCD that I got was also an unexpected (but plesant) surprise: it came with the PCF8574 component (a component that allows for more GPIO pins) already soldered onto the LCD1602.  After realizing that this aligned with my PCB schematic, I gladly deleted the PCF8574 from my schematic and PCB Editor, and more configuration was done.

<img width="336" height="394" alt="image" src="https://github.com/user-attachments/assets/160a036f-f38c-4282-8fc8-6b0d2da49ddb" />

Due to the unique pin that the LCD came with, however, I had to redo the footprint for the LCD as well.

<img width="953" height="347" alt="image" src="https://github.com/user-attachments/assets/48bfe19e-669a-4a39-8fe7-675b7aaf8309" />

<img width="677" height="423" alt="image" src="https://github.com/user-attachments/assets/7f27a420-fbc6-4b69-8d8e-b9f9572b44ae" />

## V0.5
Reviewing my the PCB, I realized that the 5V pin on the LCD wasn't connected to anything, and thus began the **third** reexamination of my PCB's power management.  After scrutiny, I fixed the 5V pin on the LCD fairly quickly (connect the 5V on the LCD to the VBUS pin on the XIAO), but there was another issue that I found, and it had to do with the BSS138 components.  BSS138s are what are called "bidirectional I2C level shifters", which means they mediate the translation between a higher voltage (e.g. 5V) and a lower voltage (3V).  Cleaning up my schematic to mitigate risks of making errors due to confusion, I then revised the BSS connections.

<img width="839" height="347" alt="image" src="https://github.com/user-attachments/assets/942dafe6-9980-449b-8c2b-b74725dc3ee8" />

Once again, I had to rewire everything (BSS138 is a surface-mount/SMD component, which made rerouting a little harder).

<img width="776" height="473" alt="image" src="https://github.com/user-attachments/assets/953cdc1b-8b1c-4cba-a620-0a88c0e12b7a" />

I also noticed that I really needed a 3D model for the LCD component, becasue that was not only the biggest part, but it's also one of the most important parts when it came to me designing a housing/case for my PCB.  Surfing through the internet, I landed upon a sketchy-looking 3D model of the exact same component (I copied and pasted the Amazon name of the component into Google), and it was in some Autodesk-specific file format.  After registering for a free trial for Autodesk products (specifically Fusion 360), I converted into an .stl file and imported into OnShape to look at it further.  The model  wasn't that bad, and when I linked the 3D model to my LCD footprint on the PCB in KiCad, it fit right in!
One tiny change had to be made, and it was the deletion of the right-angle pins (I bent the pins on my LCD to make it straight to make it parallel to the PCB surface...I hope that doesn't mess up dimensioning...)

## V1.0
Remember the 16-pin connector that I mentioned?  Their job was to act as pins that wires from the AudioJack breakout module could connect to, but seeing as to how it adds unnecessary space to the Walkman, I designed the AudioJack component as a footprint in the PCB Editor to get rid of the 16-pin connector (this did in fact save a lot of space).  This required some dimensioning, which I did, and I made a rough OnShape model of it.  Exporting it onto the 3D Viewer in my PCB Editor on KiCad, I moved it up a bit (which will represent me using pinn connectors to elevate it) in order to give it some room so it doesn't collide with the right-angle switches.

<img width="467" height="480" alt="image" src="https://github.com/user-attachments/assets/7d0dcfdc-7590-4fc6-a879-fd2b8a7225ce" />

<img width="726" height="477" alt="image" src="https://github.com/user-attachments/assets/d0452796-af9d-4948-b302-43310ac3fb66" />

I utilized my 3D printer to print simplified versions of my PCB to check the footprints and pin dimensions for the XIAO, LCD component, and AudioJack component (not pictured), but after verification I ordered the PCB from JLCPCB, and now I wait for it to come (as well as some other LCSC components).

<img width="634" height="456" alt="image" src="https://github.com/user-attachments/assets/eda2f244-dacc-4cd8-92e5-dad808207020" />

<img width="344" height="409" alt="image" src="https://github.com/user-attachments/assets/307fef49-f7a5-409d-bd6a-d79b114bcaa6" />

# BOM (not including delivery fees + tariffs)
| Id      | Name    | Vendor  | Qty     | Cost |
| --- | --- | --- | --- | --- |
| 1 | [microSD card slot](https://www.digikey.com/en/products/detail/molex/0472192001/3044807) | DigiKey | 10 | $14 |
| 2 | [BSS138](https://www.digikey.com/en/products/detail/onsemi/BSS138/244210)| DigiKey | 10 | $2 |
| 3 | [Power Switch (taken from my friend's recommendation)](https://www.lcsc.com/product-detail/Slide-Switches_C-K-OS102011MA1QN1_C226259.html) | LCSC | 10 | $5.25 |
| 4 | [XIAO ESP32S3](https://www.amazon.com/ESP32S3-2-4GHz-Dual-core-Supported-Efficiency-Interface/dp/B0DJ6NQFKX/ref=pd_rhf_dp_s_ci_mcx_mr__d_sccl_1_1/137-7709202-3397348) | Amazon | 3 | $27 |
| 5 | [1602 LCD + PCF 8524 module](https://www.amazon.com/Hosyond-Display-Module-Arduino-Raspberry/dp/B0BWTFN9WF/ref=pd_rhf_dp_s_ci_mcx_mr__d_sccl_1_3/137-7709202-3397348) | Amazon | 3 | $14 |
| 6 | [AudioJack + PCM 5102 module](https://www.amazon.com/PCM5102-PCM5102A-Digital-Converter-Raspberry/dp/B0DNW32Y46/ref=sims_dp_d_dex_ai_rank_model_1_d_v1_d_sccl_1_3/137-7709202-3397348?psc=1) | Amazon | 2 | $9 |
| 7 | [1000mAh LiPo battery](https://www.amazon.com/1000mAh-battery-Rechargeable-Lithium-Connector/dp/B07BTWK13N) | Amazon | 1 | $9 |
| 8 | [Right-Angle Switches](https://www.lcsc.com/product-detail/C49101620.html?spm=wm.ddx.0.xqy___wm.ddl.ddb.0.ddh&lcsc_vid=ElUPAwcDQFlaVF0HQ1dXAwFXFVNbUVFeQFIPBQIHQgQxVlNeR1FZVVVQR1laVTsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktSR1RADxALGw%3D%3D) | LCSC | 50 | $0.63 |
| X | X | X | X | ~$81 |

## Additional supplies

I started to get soldering supplies by asking my friend's dad for some, to which he responded with a simple roll of solder and an okay soldering iron.  This worked out fine for the simpler components, but when it came to more complex soldering assemblies such as SMD components, I needed help.
After some discussion with by more-experienced friend, he told me that I needed a pack of liquid/solid flux (just in case if the rosin-core solder didn't have enough), a heatbed for the SMD components, and some solder paste to complement the heatbed for easier soldering for SMD components.
| Id      | Name    | Vendor  | Qty     | Cost |
| --- | --- | --- | --- | --- |
| 1 | [Heatbed](https://www.amazon.com/Soldering-Microcomputer-Technicians-Electronics-Enthusiasts/dp/B0G443BG4X/ref=sr_1_2?sr=8-2) | Amazon | 1 | $27 |
| 2 | [Flux](https://www.amazon.com/SRA-Soldering-Electronics-Lead-Free-Electrical/dp/B008ZIV85A/ref=sr_1_6?crid=3PSC9N7K6VI1P&dib=eyJ2IjoiMSJ9.4lAJRvPbs-mZfOjdNN3yko1QdCRJ7DuF7ITQXP00Zw6-YTXEtz6O56z-3mFeA06DFWn7K46TQMWEEocoB24hUeA2pRWL5PZLodoffU67bT22aAduVxkx_wdd-4mv4hNAZPr-tqz4AYCK0zWmtre61fzN7fRagjiYjk4f0m6PkqVZ_U-DropUBjAUAZUFRuWYf_Zg6Ls1t9Iee1CwaPx7wRCERDrgLYxmO5XsuhNiYI31TFE8GYnA0AEQibicbohzDRZsgtbbjuhwPmBq9184HANk6QaEDnCSlJgSGyVij_4.RXMTRwdvJQXcmnfBtIILk3Vw2HaX5XoBBaaOHqvCQDs&dib_tag=se&keywords=solder+flux&qid=1787439264&sprefix=solder+flu%2Caps%2C151&sr=8-6) | Amazon | 1 | $9 |
| 3 | [Solder Paste](https://www.amazon.com/Particle-Melting-Electronics-Welding-100G/dp/B0FYH9HS2W/ref=sr_1_24?crid=1XXM8RE6MJU3V&dib=eyJ2IjoiMSJ9.RM36QPd0a2H4_bdhGSOKfZJjHoW4TT7FYbYOePXYuUSKFAHb8I43R-8Ku84GS6KqnE81AwtSetvDehl8jUrOpetkE9Lp1e0oAUrra1Ax1yHaP54gxSOjCNy8Qae3zJZ3lqb1vRmu-jv4T_6l-unRR69yQe7E2hoBbOXNDQxANlSyCc-yngeB1UcluzowntyGix_HBKZ0-sbckXMkqIkEe25zazsldICJT3-jejK2Nnjor7P6o3duiNHdLID88EolUzPUfiM_pN3laRQF3XeSDC66AEbr2nc3RMiYHQiKlFM.QaV3XLYiIFU6J7uR8jqXOCL1FU7gVYKlh0sjLuVEvP0&dib_tag=se&keywords=solder+paste&qid=1787439314&sprefix=solder+pas%2Caps%2C222&sr=8-24) | Amazon | 1 | $22 |

After getting these components, I set up shop in my garage, and I opened the garage door so that the yummy lead fumes could escape.  However, I got moved to my back patio after my dad complained after a bunch of bugs came it in from the open garage door.

Finally, after having done most of the soldering to enable theoretical functionality for my Walkman, I tried hooking it up to my computer using a Logi USB-C cable, and after some vibecoding with Claude Opus, I got the Walkman to work...partially.  The display was a little off, and no matter how many times I unplugged and replugged my earbuds, I still couldn't hear anything from the Walkman.  Thankfully, the microSD card reader was working, as well as the LCD after some adjustment, because I saw it displaying the text of the songs that I had loaded onto the microSD card.

Switching out my earbuds for headphones that I usually use, I was finally able to hear the music that was playing!
<img width="2160" height="2880" alt="image_2" src="https://github.com/user-attachments/assets/d85f2e68-401e-4ce1-a042-2031f7e108c1" />
<img width="2880" height="2160" alt="image" src="https://github.com/user-attachments/assets/83144d3e-38c6-4d2d-a16f-798502de3260" />

However, the battery still needed to be implemented into the Walkman PCB, and I soon realized that the V1.0 Walkman PCB wouldn't be able to distribute the LiPo battery's power to all the peripherals on the PCB.  This was because I wired the AudioJack, LCD display, and all the other peripherals other than the microSD card to all use VBUS (5V) power instead of 3.3V power.  The problem lied in how the 3.3V pin, not the VBUS pin, was the only power distributor when the Walkman is disconnected from the XIAO's USB-C's power source.

## V2.0 
With the LiPo power distribution not working and the LCD screen not being entirely accurate to Makoto's Walkman in Persona 3, I returned to the drawing board that is KiCad.  By working with Claude, I found another [LCD screen](https://newhavendisplay.com/2x20-character-lcd-stn-gray-display-with-side-white-backlight-and-pin-header-3v/) online that looked more similar to Makoto's Walkman screen.  Looking at its datasheet, I tried adding it into my Walkman PCB schematic.
