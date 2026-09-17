# DTU Ballerup PCB prototyping
Guide for producing PCB's from KiCad with DTU Ballerup equipment. 

<br>

## What will you need?
- [KiCad 9.0+](https://www.kicad.org/download/)
- A **single-sided**[^1] copper PCB FR4 board.
- Design your PCB with the footprints listed in the [footprints table](footprints_table.md).
- Have participated in the safety course held by the professor or TA's.

<br>

## Contents
- [What to keep in mind](#what-to-keep-in-mind)
- [Making PCBs with the Fiber laser](fiber_laser_guide.md)
- [Making PCBs with the Roland CNC router](roland_cnc_guide.md)

<br>

## What to keep in mind
PCB's made in the course [62733](https://kurser.dtu.dk/course/62733) should preferably be made as **one-sided** PCB[^1]. Therefore, make sure to do all of your traces on the back side layer (B.Cu) in the KiCad PCB Editor:
![Design note 1](images-for-guides/kicad_design_note1.png "Design note 1")
> [!TIP]
> A quick way to check if you have selected the correct layer is, if the traces drawn becomes blue.
>
> If your traces are red, then you have selected the top layer (F.Cu).

It can also be a good idea to increase the size of traces for easier result consistency[^2].
> [!IMPORTANT]
> This step should be done **before** designing your PCB.
>
> It is **not possible to do afterwards.**

**To do so, do as shown in the *GIF*:**
1. Go into *Board Setup*, by clicking the small green circuit icon next to the save button.
2. Choose the *Net Classes* option under *Design Rules*:
3. Change *Clearance* to **0,8 mm** and *Track Width* to a minimum of **0,8 mm**, if possible then 1,0 mm and larger is prefered for working with most through-hole component PCB's made on the Fiber laser and CNC router.

![Kicad netclasses](images-for-guides/kicad_net-constraints.gif "Kicad netclasses")


<details>
  <summary><b>Step by step with pictures</summary>
  
   1. Go into *Board Setup*, by clicking the small green circuit icon next to the save button.

   ![Design note 2](images-for-guides/kicad_design_note2.png "Design note 2")

   2. Choose the *Net Classes* option under *Design Rules*:

   ![Design note 3](images-for-guides/kicad_design_note3.png "Design note 3")

   3. And change both *Clearance* and *Track Width* to 0,8 mm **minimum**. 1,0 mm and above, if possible, is prefered for working with most through-hole component PCB's made on the Fiber laser and CNC router.
  
</details>




<br>



### Preparing your PCB

The most important step before going out and making or buying a PCB, is doing the your basic checks you learned in the course!
- Have you used the correct footprints?
- Have you designed your PCB on the correct size, and not flipped any components?
- Have you tried running the *Design Rule Checker* (DRC)?
- Have you added your own PCB board cutout in the `Edge.Cuts` layer?
If any of these steps have been skipped or done incorrectly, then making the PCB is a waste because its likely not working once you have it in your hand.

Before going out to find and cut a bare PCB board, take some measuments of your design in KiCad so you know how big to cut your PCB on the shear. Be sure to not going too tight with your measurments. Add around 2mm to your total width and length, so you don't risk your final board coming out too small.
![KiCad measuring](images-for-guides/kicad_measuring.gif "KiCad measuring")

When finding a bare PCB board:
- **Please don't use the boards with the blue film on**. They are not meant for the Fiber laser.
- Do not take a double-sided PCB board.

Ask for a proper bare PCB board if you are not able to find one.

After cutting your board to the correct size (plus your added 2~mm padding), take some 400 grit sandpaper and brush the surface a bit. **Don't overdo it!** We just need to remove the protective/oxide layer before moving onto the Fiber laser.


---


[^1]: Currently we are limited to one-sided PCB's until further testing and workflows are prepared. The students are free to try their hand ad two-sided PCB's, but should then consult with the people responsible for the machines, and it will be at their own risk and time.

[^2]: This step is only necessary for PCB-milling and Fiber-etching.


