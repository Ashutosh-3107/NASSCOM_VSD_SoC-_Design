## Clone the std cell from the github repository

```
cd ~/Desktop/work/tools/openlane_working_dir/openlane
git clone https://github.com/nickson-jose/vsdstdcelldesign.git

```

## View the std cell in magic

```
cd ~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
ls -ltr
magic -T sky130A.tech sky130_inv.mag &

```
![Screenshot 2024-03-17 164622](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/3bbf88b1-c1af-4f46-b82e-8938d10bb74e)


### Layers and connections of the std cell

Hover over the various diffusion layers , press s and then enter what in the tckon console window to find out the layers and the connections

![Screenshot 2024-03-17 202954](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/ef46b59c-3bc8-4b32-863c-d19747bafb37)

![Screenshot 2024-03-17 203034](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/fc2574e5-9f1b-4d30-a696-4e1b37aa9474)

![Screenshot 2024-03-17 203148](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/47a00b7e-820f-4099-8256-12808c2faa81)

![Screenshot 2024-03-17 203231](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/3b6a9d91-cfc8-46ea-8f51-13ec15f06ac4)

![Screenshot 2024-03-17 203252](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/f67604e8-e01e-4063-9b29-6b614853533b)

##Extracting as a spice file

1. In the tckon window console enter

```
pwd
extarct all
%ext2spice cthresh 0 rthresh 0
%ext2spice 

```

![Screenshot 2024-03-17 204430](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/eae2578b-877c-4204-b438-98bc2241e58f)

2. View the spice netlist code

![Screenshot 2024-03-17 204524](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/7bc0dd21-c6a3-4f76-9099-6b3d48d05319)

3. Modify the spice netlist by finding the scale of the grid in the inverter layout

   ![Screenshot 2024-03-18 195250](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/da79fed0-c683-46c9-b70f-8d6fdd01f3ad)

   ![Screenshot 2024-03-18 113540](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/1ee274eb-cc53-4fa6-8d47-184bc6815f03)

4. Modify the code using the text editor

  ![Screenshot 2024-03-25 215404](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/e626ecad-4bd5-406b-a744-266960fe7485)
 
5. Using the tool ngspice source this edited spice file and run the simulation


   ```
   sudo apt-get install ngspice
   ngspice sky130_inv.spice

   ```

   ![Screenshot 2024-03-18 194907](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/416e5c61-9378-4666-a5e7-6b32176aea0d)


   ## Steps to characterize the cell

   1. In the ngspice simulator
  
      ```
      plot y vs time a

      ```

      ![Screenshot 2024-03-18 195937](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/c188fb8f-e86e-4d6f-a2a5-50cf2c143d97)

2. To zoom in a particular region right mouse click that region and find the respective parameters

   ![Screenshot 2024-03-18 201115](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/cb29ea19-2a9f-434f-8e77-433704d2341e)

3. Find the rise time and fall time of the cell , pointing to the regions

   ![Screenshot 2024-03-18 201916](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/df81a43e-4d0e-4eef-9b89-d806bf4d4ccf)

   Rise time  = 0.05869

   Fall time  = 0.05724


   ## Fixing DRC error in magic

 1. clone the files for this lab from the following url

   ```
   wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
   tar xfz drc_tests.tgz
   cd drc_tests

  ```
2. Open the magic tool

  ```
  magic -d XR

  ```
3. Load the poly.mag file from the tckon window

   ![Screenshot 2024-03-18 210603](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/fa033b6b-70e6-4d1c-bf99-b36552d00e37)

   ![Screenshot 2024-03-18 210437](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/f728d9c2-b242-4c06-b792-e48add6502cc)


4. Hover over the poly and the npoly res to view them on the tckon window

   ![Screenshot 2024-03-18 210702](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/4e42a925-8aa8-494f-8bbd-62205a1c325c)

5. Make a box between them and view the spacing. This spacing is not according to the drc rules.

  ![Screenshot 2024-03-18 210939](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/18c43c1b-b83a-462f-8491-575654d27113)

6. Using the text editor fix the distance between the poly and the polyres

   ```
   vi sky130A.tech

   ```

   ![Screenshot 2024-03-18 214231](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/fd9c6a79-ff0f-42db-967c-ad4b61113edc)

   ![Screenshot 2024-03-18 214342](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/30ff0a93-b36b-423f-8994-4a85a4e5cae0)


7. Close the magic and run the following commands to observe the change

   ```
   drc check

   ```

   ![Screenshot 2024-03-18 221909](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/01449cf0-d924-4c9d-acef-c9f44d9f45a4)

8. The DRC error is now fixed

   ![Screenshot 2024-03-18 221215](https://github.com/Ashutosh-3107/NASSCOM_VSD_SoC-_Design/assets/159696526/cd90366c-d06a-46b6-b261-e48a36b71393)




 



   









