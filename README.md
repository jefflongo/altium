# Altium
A collection of standardized Altium libraries and DRC rules collected over time. Below are the repository guidelines.

## Schematic Libraries
* Schematic libraries are to be named `Schematic_Category.SchLib` where `Category` groups parts with similar function (diode, MCU, connector, etc).  
* Each part is to be populated with parameter, descriptive, and ordering information using Altium's manufacturer part search feature. The symbol itself should not contain vendor-specific information (such as vendor part number).
* Do include information such as I2C addresses, or anything else that might be useful on the symbol.
* Inputs should be on the left side of the part, and outputs should be on the right side of the part for parts with obvious input-output relationships.
* Related pins should be grouped together on the schematic symbol (see the `Group` column if using the Schematic Wizard). 
* For parts with a large pin count, the schematic symbol should be separated into multiple component parts. Consider splitting on groups such as power, I/O, etc.

## Footprint Libraries
* Footprint libraries are to be named `Footprint_Category.PcbLib` where `Category` groups parts with similar function (diode, MCU, connector, etc).
* Footprints should be created using the IPC Compliant Footprint Wizard whenever possible, generating a STEP 3D model. Although the wizard may suggest a land pattern based on the part dimensions, these should be overridden with the manufacturer's recommended land pattern when applicable.
* If the IPC Compliant Footprint Wizard cannot be used, `Template_Footprint.PcbLib` should be used as a template to build the footprint, following the recommended land pattern in the part data sheet.
* All footprint origins should be placed at the center of their part's bounding box.
* Footprints should inherit the suggested name if using the IPC Compliant Footprint Wizard, otherwise use the manufacturer's part name.
* All footprints should follow the following component layer pair/mechanical layer configuration. Note that parts using the IPC Compliant Footprint Wizard will likely need portions moved from mechanical layers to component layer pairs following the style below.
  * Component Layer Pairs (must be layer type assigned)
    * Overlay
    * Solder
    * Paste
    * **Assembly** on layers M2/M3
    * **Courtyard** on layers M4/M5
    * **3D Body** on layers M6/M7
  * Mechanical Layers
    * **Mechanical 1** (used only for board cutouts)

### Layer Guidelines
Assembly
* The assembly layer should contain an 0.1mm line width rectangle sized to be the bounding box of the part (**not pad**) dimensions.
* The assembly layer should also contain a center justified string `.Designator`, at the part center, with height and stroke width appropriate such that the string is easily readable and 4 characters do not intersect the aforementioned bounding box.
  
Courtyard
* The courtyard layer should contain an 0.1mm line width cross (two perpendicular 1mm lines, shorter if necessary) at the part center.
* The courtyard layer should also contain an 0.05mm line width rectangle sized to be 0.25mm larger on each size of the bounding box of **the greater of the part and pad dimensions**.
  
3D Body
* The 3d Body layer should contain an accurate 3D model of the part if available. An attempt should be made to search for a 3D model if the IPC Compliant Footprint Wizard cannot be used.

Mechanical 1
* Mechanical 1 should contain any board cutouts required for the part. This layer, or any other mechanical layer, should not be used otherwise.
  
Overlay layers
* Overlays should use 0.2mm line width if possible, should be adequately spaced from any solder mask expansions, and should clearly indicate pin 1 if necessary.
