# DTU-pcbCNC (This part of the project is archived and not to be used for actual PCB prototyping)

Various project files for the Bungard CNC pcb router at DTU

## Dependecies

- KiCAD 8.0+
- Python 3
- [pcb2gcode](https://github.com/pcb2gcode/pcb2gcode)

## How to make a program for the machine (Linux):

Currently the procedure is very clunky and not meant actual production. It is only tested on Linux, and will only be, until proper testing and transition to a dedicated solution.

> [!WARNING]
> **It requires manual editing of files from both KiCAD and pcb2gcode.**
>
> **This is merely a documentation of the steps required until an intuitive easy procedure is made.**

### Step 0. When making PCB's with KiCAD.

For *one-sided* PCB's you need to place all of your routes on **B.Cu** (Backside) and **not flip any components**.

*Two-sided* PCB's has **not been tested yet**, so should therefore not be attempted.

Do not use *Filled zones*. We will only machine around traces, which would render *Filled zones* pointless for saving time.

Recommended *Board Setup* settings:

- Clearance: minimum 0.7mm.
- Track Width: 1mm.

### Step 1. Export files from KiCAD.

1. In the *PCB Editor*, go to `File` - `Fabrication Outputs` - `Gerbers (.gbr)...`
2. With the *Plot* window open, choose the `Plot format:`to `Gerber`, and deselect everything in the *Include Layers* section, except `B.Cu` and make sure that `B.Cu` is the **only selected** layer.
3. In the *Plot on All Layers*, everything should be **unselected**.
4. In the *General Options*, make sure that the settings are set as follows:
   - `Plot drawing sheet` = unselected.
   - `Plot footprint values` = unselected.
   - `Plot reference designators` = unselected.
   - `Plot footprint text` = unselected
   - `Force plotting of invisible values / refs` = unselected.
   - `Sketch pads on fabrication layers` = unselected.
   - `Check zone fills before plotting` = unselected.
   - `Use drill/place file origin` = **selected**.
   - `Tent vias` = unselected.
   - `Use Protel filename extentions` = unselected.
   - `Generate Gerber job file` = unselected.
   - `Subtrack soldermask from silkscreen` = unselected.
   - `Coordinate format:` = `4.6, unit mm`.
   - `Use extended X2 format (recommended)` = **unselected**.
   - `Include netlist attributes` = selected.
   - `Disable apature macros (not recommended) = unselected`.
5. Select an output directory to store the saved files, by clicking on the folder icon in the top right corner, and choose a location.
6. Now click on the *Plot* button in the bottom right corner. Make sure the message in *Output messages* says `Done.` and that there is no errors occurring.
7. Click on *Generate Drill Files* in the bottom right corner.
8. In the *Generate Drill Files* window, make sure that the settings are as follows:
   - `Drill File Format` = *Excellon*
       - `Mirror Y axis` = unselected.
       - `Minimal header` = unselected.
       - `PTH and NPTH in single file` = unselected.
   - `Oval Holes Drill Mode` = *Use route command (recommended)*
   - `Map File Format` = *Gerber X2*
   - `Drill Origin` = **Drill/place file origin**
   - `Drill Units` = **Millimiters**
   - `Zeros Format` = *Decimal format (recommended)*
9. Now click on the *Generate Drill File* button in the bottom right corner. Make sure the message in *Output messages* says `Done.` and that there is no errors occurring.

### Step 2. Download and setup necessary generators and parser.

To be added..

### Step 3. Generate base Gcode.

```bash
pcb2gcode \
--back *-B_Cu.gbr \
--drill *-PTH.drl \
--outline *-Edge_Cuts.gbr \
--output-dir=./CAM-exports/ \
--cut-side=back \
--drill-side=back \
--cutter-diameter=0.75mm \
--zsafe=5mm \
--zchange=30mm \
--zwork=-0.1mm \
--mill-feed=2 \
--mill-speed=20000 \
--metric \
--metricoutput=1 \
--zdrill=-5mm \
--drill-feed=50mm/min \
--drill-speed=20000 \
--zcut=-2.5mm \
--cut-feed=30mm/min \
--cut-speed=16000 \
--cut-infeed=20mm \
--bridges=0.5mm \
--bridgesnum=3 \
--zbridges=1mm \
--zero-start=1
```

## Current ATC setup
The router is equipped with an ATC (Automatic Tool Changer), which gives us the option of machining *and* drilling all of PCB holes in one setup.

> [!CAUTION]
> These tools are not meant to be changed by the user! These should only be changed by the people responsible for the machines service and upkeep!

> [!IMPORTANT]
> If you break one of the tools, please contact one the people responsible for the machine, or **at the very least place a note on the machine about which tool is broken**.


| Tool number | Tool description | Tool max depth | Spindle speed | Radial feed speed | Axial feed speed |
|-------------|------------------|----------------|---------------|-------------------|------------------|
| T00 | Test tool (DO NOT REMOVE OR CHANGE!) | --- | --- | --- | --- |
| T01 | 30° V-bit - Ø 0.75 mm | 0.1 mm | 30 000 rpm | 50 mm/min | 20 mm/min |
| T02 | 2-flute endmill - Ø 2.00 mm | 2.5 mm | 30 000 rpm | 50 mm/min | 20 mm/min |
| T03 | Ø 0.7 mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T04 | Ø 0.8 mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T05 | Ø 1.0 mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T06 | Ø 1.3 mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T07 | Ø 1.5 mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T08 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T09 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T10 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T11 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T12 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T13 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T14 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
| T15 | Ø --- mm drill | 2.5 mm | 30 000 rpm | --- | 200 mm/min |
