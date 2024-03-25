# Floorplan 

## Steps
1.Set the following parameters in the design config.tcl 

```
set ::env(FP_CORE_UTIL) 65
set ::env(FP_IO_VMETAL) 4
set ::env(FP_IO_HMETAL) 3

```
![Screenshot 2024-03-17 123120](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/fe38eb65-0a81-4d3d-9e6e-32cfaac3840f)


2. Set the following parameters in the library config.tcl

   ```
   set ::env(FP_CORE_UTIL) 65

   ```
   ![image](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/dbada0d1-08f8-439e-9a2a-a786a52a12d0)


3. The above variables which are set are reflected in the runs config.tcl file. To view it

   ```
   cd ~/Desktop/work/tools/openlane_working_dir/designs/picorv32a/runs/run1/
   gedit config.tcl

   ```
![Screenshot 2024-03-17 123313](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/3d60a547-b9c1-4c51-b7c5-eff46502a345)

4. Go to the openlane flow as described in day 1. After running synthesis, give the command

   ```
   run_floorplan

   ```
## View the floorplan def
1. Enter the following commands in the terminal
   
```
cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/run1/results/floorplan/
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sk130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def reaf picorv32a.floorplan.def &

```

2. Go the magic window and center the layout by pressing s and then v


   ![Screenshot 2024-03-17 124349](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/5a3d9f30-8740-446a-968e-beed13ae96af)


   Then hover the cursor over the horizontal and vertical pins and in the tckon window of magic write
   ```
   %what
   ```

   You will observe the metal layers to which the pins are attactched getting displayed

   ![Screenshot 2024-03-17 123935](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/014545a4-9c87-429c-bc74-14d17da1a998)

   ![Screenshot 2024-03-17 124055](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/e13ee6d2-16ae-42da-82b9-dcd26cff6144)



3. You can also view the macro std cells by zooming in

   ![Screenshot 2024-03-17 124330](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/55f14ee8-41b4-4b0e-a7c6-1e425be9e385)

   ## IO Placer log

   ![Screenshot 2024-03-17 123410](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/15d06c52-2f0b-48d1-95e3-060a81344877)


   # Placement

   1. Steps for placement

      ```
      prep -design picorv32a -tag run1 -overwrite
      run_synthesis
      run_floorplan
      run_placement

      ```

   2. View placement using magic

      ```
      cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/run1/results/placement/
      magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sk130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def reaf picorv32a.floorplan.def &

      ```

      ![Screenshot 2024-03-17 130608](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/8ecbc1b7-92f1-4efc-8d51-a33db23f5428)


   3. View placement log

      ![Screenshot 2024-03-17 125821](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/b5a294d9-d878-4489-bef8-f0aa1670ccc3)



   # IO PLACER REVISION

   1.  During the openlane flow you can set the following input output strategy

     ```
     set ::env(FP_IO_MODE) 2

     ```

    ![Screenshot 2024-03-17 131905](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/0114ac1e-2f54-45fe-aa06-ae57e42f740f)


   2. View the def file similarly as mentioned above

      ![Screenshot 2024-03-17 132511](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/c2c523f9-3270-4e34-ad06-30fc9ec87fb1)


      ![Screenshot 2024-03-17 132540](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/4dc6512f-2045-4e7c-9940-56364b1de823)
 
 

   


  
      




   


   
