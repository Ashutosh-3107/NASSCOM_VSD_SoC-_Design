# Synthesis

## Steps
Steps to run synthesis of the RTL code of Picorv32a

```
cd ~/Desktop/work/tools/openlane_working_dir/openlane/
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a -tag run1
run_synthesis

```

### config.tcl file
![Config_tcl](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/29433463-6302-4d32-978b-bd2a3a4168f8)

#### library config.tcl file
![library_config_tcl](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/86f42bd6-c915-46fe-9fef-430b5d4233a2)

##### OpenLane flow
![Openlane_flow_tcl](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/d6851f16-9f89-426c-845c-0931bfa2ba67)

###### Merging lef files
![Merge_tech_lef_files_1](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/999535b8-8752-4bd5-8595-038b0cc33f2c)

## Synthesis Report
![Flop_Ratio_1](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/0a6ecfb2-79c2-4df5-a36b-d7ee16d5b968)




![Flop_Ratio_2](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/95f4c194-dd7c-4dc5-9871-b9b27b5756d8)

### Flop Ratio
 No. of cells = 14876
 
 No. of D-flip flops = 1613 
 
 Flop Ratio = No. of D-flip flops / No. of cells 
 
            =1613/14876 
            
            =0.1084 
            
## Sta log

![Sta_log](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/96988e9c-94d2-4a64-b794-7ac7c38bb650)

tns = -759.46

wns = -24.89

## Mapping of RTL to internal library

![Screenshot 2024-03-25 193041](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/d0d5b385-0614-4c0b-9ffb-08b630272c45)


![Screenshot 2024-03-25 193057](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/74cb07fb-0f38-4cfe-872b-88d568808a68)








