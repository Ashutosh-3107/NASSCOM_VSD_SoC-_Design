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

## SDC Files

### pre_sta.conf

![Screenshot 2024-03-23 202004](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/3f8e5b94-a984-4af6-b4fa-4f221ba7ef91)

### my_base.sdc

![Screenshot 2024-03-23 202557](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/4bcabdbb-713f-4ecd-85c2-54b0d7b27202)

![Screenshot 2024-03-23 202608](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/9229c229-4382-4761-ac77-99baa0ab53bb)

## Reducing the slack to zero

We may not require the above files to reduce the slack to zero. Following are the steps to reduce the slack to zero
```
prep -design picorv32a -tag run1 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_STRATEGY) "DELAY 0"
set ::env(SYNTH_SIZING) 1
run_synthesis

```
![Screenshot 2024-03-22 133842](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/e55e5cf6-2770-4f84-979b-fc6fba9c07f5)

![Screenshot 2024-03-22 133939](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/dcfa2bde-ec09-4602-bf0f-8184fcadff13)

Area of the chip has increased

tns = 0.00

wns = 0.00

## Floorplan and Placement

run_floorplan may result into error. Another alternative is to go to the tcl_commands/floorplan.tcl and view all the sequential procs that take place and give that procs as commands one by one during the openlane flow

```
init_floorplan
place_io
global_placement_or
detailed_placement
tap_decap_or
detailed_placement

```

The def file can be viewed using the magic layout tool

![Screenshot 2024-03-23 153423](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/bdbbe50f-cbf7-4aaf-ad79-7de92021f611)

![Screenshot 2024-03-22 135109](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/8c9bde90-d5c4-4f6f-9fd0-163a122fe9bb)


## Clock-tree Synthesis

Continuing simply give the command run_cts

Following output will be shown after running the clock-tree synthesis

![Screenshot 2024-03-23 211238](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/9d57dc39-aa42-4457-92b9-a5161b948e32)

![Screenshot 2024-03-23 211300](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/c488d0c1-393c-4ca7-9d2d-182052b38625)

![Screenshot 2024-03-23 211310](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/3b6c6778-7ec0-4dea-8bb8-0d4cc6ff4b97)

![Screenshot 2024-03-23 211520](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/2e4afcea-555c-41c2-9dad-f048740a6dc8)

## Post Clock tree synthesis

We invoke openroad in the openlane flow
```
%openroad

```

Run the following commands to create a .db file which the openroad software can read

```
read_lef /openLANE_flow/designs/picorv32a/runs/run1/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/run1/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/21-03_02-34/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_TYPICAL)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/picorv32a.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pin} -format full_clock_expanded -digits 4

```

Replace the clock buffer by giving the following command

```
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

```

We observe the output as

```
sky130_fd_sc_hd__clkbuf_2 sky130_fd_sc_hd__clkbuf_4 sky130_fd_sc_hd__clkbuf_8

```

![Screenshot 2024-03-24 120232](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/a8697735-14e8-4d42-8688-d7ac3246ca26)

Commands to report the skew

```
report_clock_skew -hold
report_clock_skew -setup

```


![Screenshot 2024-03-24 120653](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/919ae189-4d6e-4a89-8358-ceab5c248a98)

## Layout after CTS

![Screenshot 2024-03-24 122603](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/3549224f-6ef6-4ae4-a412-d04bc299117a)






















 





