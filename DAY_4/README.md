## Converging the grid definition into track layer info

![Screenshot 2024-03-19 100758](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/a777a6b5-3685-4485-a3a5-9cbaaebbf38d)

![Screenshot 2024-03-19 101155](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/586d1d45-68c9-4be1-8a78-7243023d1b24)

The place and route tools use this grid info

![Screenshot 2024-03-19 101417](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/ec2a0c4e-ab0e-4057-b8b7-7c9386f54619)

## Creating port definitions

 In Magic Layout window, first source the .mag file for the design (here inverter). Then Edit >> Text which opens up a dialogue box. All these definitions have already been set.

 ![Screenshot 2024-03-19 101506](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/dff46849-a491-49bb-aa77-aa374b343f12)

 ![Screenshot 2024-03-19 101724](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/1774b3ba-3ce8-4bd0-80b8-df47670d46cf)

 ![Screenshot 2024-03-19 102046](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/93c89989-3710-48ed-a5f6-a1b53a4b4424)


## Set port class and port use attributes for a layout

Post port definition, the next step is setting port class and port use attributes. All these definitions have already been set

![Screenshot 2024-03-19 102921](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/d3f5bbe6-4f17-4093-8af2-6ba494dbbd91)

## Extracting LEF file

Once the properties are set,
```
lef write

```
command writes the LEF file with the same nomenclature as that of the layout (.mag) file.

![Screenshot 2024-03-19 102744](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/5bcd4943-f53a-4556-8f21-a8b2d88cdfb5)


## Importing files

Copy the extracted lef file and sky_fd_sc_hd__.lib * all files from vsdstdcelldesign into the design folder of picorv32a/src and make the following changes to the design config.tcl file of picorv32a

```
set ::env(LIB_SYNTH) "$:env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$:env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$:env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$:env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

```
![Screenshot 2024-03-19 110404](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/33f9e771-e7a9-4bf8-af99-2725b89079f9)

## Open Lane flow

We will now incorporate the vsdstdcell in the picorv32a

```
prep -design picorv32 -tag run1 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```
![Screenshot 2024-03-21 152701](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/dd5adf68-eea0-4fa8-ba80-280aa0a215b1)

![Screenshot 2024-03-19 110615](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/d248a260-7876-4205-82da-c09ddafdacc9)

We can see vsdstdcell has been incorporated in our design








 





