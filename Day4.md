# VSDIAT SKY130 DAY 4 : Pre-Layout Timing Analysis and Importance of Good Clock Tree

## Timing Modelling Using Delay Tables

### Lab Steps To Convert Grid Info Into Track Infor

<img width="1440" height="266" alt="image" src="https://github.com/user-attachments/assets/2e74bcfa-f87e-4740-9742-8cef659bb1e8" />

* The content within the tracks.info file:

<img width="402" height="497" alt="image" src="https://github.com/user-attachments/assets/d9f4fd06-99f8-4a45-92bd-3c3afe4b3b33" />

* The x is **horizontal track** and y is the vertical track respectively, after that is the **orgin offset** and then it ends with the **pitch.**
* If we press g, it enables the grid in the transistor layout.

* We can hype in Help grid in the b box to view specific commands related to it that will hekp us:

<img width="1125" height="437" alt="image" src="https://github.com/user-attachments/assets/fa419031-3826-4629-9b56-b857e5fa48ab" />

* As you can see, the grid boxes have changed accordingly:

<img width="1505" height="784" alt="image" src="https://github.com/user-attachments/assets/bfc8ba9a-dc8f-46e6-9f82-5ba3d4592b71" />

### Lab steps to convert magic layout to std cell LEF

The two main guidlines are:
1. The I/O ports should intersect the x-horizontal and y-vertical tracks.
2. The height and the width of the cell should be odd multiples of the x and y. 

To define ports, we select the area and click on edit and then click on text:

<img width="1595" height="860" alt="image" src="https://github.com/user-attachments/assets/b7e51b28-1186-4e85-b562-030aebd31abf" />

  * We dont do this since its already been pre-defined for us.

We can also save the file under a new name.

As we can see the newly saved file is visibile:

<img width="1118" height="465" alt="image" src="https://github.com/user-attachments/assets/f6a03e05-1bee-4c94-b716-b88579796ae5" />

* To make an lef file, we can just type lef write (name) if we want:

<img width="1185" height="407" alt="image" src="https://github.com/user-attachments/assets/f61037e3-0439-4f48-a4c8-fe62b47f6036" />

Inside/Content of the lef file:

The pins are specified: 

<img width="777" height="892" alt="image" src="https://github.com/user-attachments/assets/bb2a63a3-d680-4bea-8cd7-d7a113734647" />

### Introduction to timing libs and steps to include new cell in synthesis

<img width="1257" height="444" alt="image" src="https://github.com/user-attachments/assets/f0cdf869-3462-473b-b301-4596a938112f" />

<img width="1378" height="869" alt="image" src="https://github.com/user-attachments/assets/4cf7a690-b3cc-4c04-aefe-d06d293edac0" />

* This directory contains special files that describe how each logic gate behaves in different conditions like hot or cold temperatures, slower or faster chips, and varying voltages. These conditions are called PVT corners. These files help tools figure out timing and power for each gate so the chip can be built correctly during synthesis.

* As we can see below, we succesfully copied the files in the .lib dir to source dir of picorv32a:

<img width="1115" height="214" alt="image" src="https://github.com/user-attachments/assets/cf377fa2-6eaf-4e2b-b165-cf179d23c375" />

* Edit and new add code to the config.tcl file like shown below:

<img width="1196" height="691" alt="image" src="https://github.com/user-attachments/assets/a13ae683-8aa2-454a-8224-3475a826c619" />

* After this, we open up docker to run openlane again, but with a bit of tweaks this time:
  * After setting up openlane normally- after the package require openlane 0.9 command, add  -tag [number run] -overwrite after the prep -design picorv32a command.
  * As you can see here:

<img width="1870" height="992" alt="image" src="https://github.com/user-attachments/assets/ed4ccbff-c887-4a18-8f7c-72cbf9e1c467" />

* Then, we type in *set lefs [glob $::env(DESIGN_DIR)/src/*.lef]* and right after that, we type in *add_lefs -src $lefs*.

<img width="785" height="195" alt="image" src="https://github.com/user-attachments/assets/9d9e0004-3128-4e3c-af4e-58075aa10c6d" />

* Then we finally run synthesis:

<img width="719" height="826" alt="image" src="https://github.com/user-attachments/assets/ab265f6d-37c9-40d1-b43b-6810a53b690d" />

### Introduction to delay tables

<img width="1107" height="508" alt="image" src="https://github.com/user-attachments/assets/49002113-fa10-44ea-8f81-d715189f4048" />

* The image above shows how clock gating works. The clock signal only passes through when the enable pin is set correctly 1 for an AND gate and 0 for an OR gate. This helps reduce unnecessary power use in clock trees by blocking the clock when it's not needed.

<img width="1557" height="645" alt="image" src="https://github.com/user-attachments/assets/8d065f9a-9590-4e4b-9b86-d8167ca2257f" />

* In real circuits, capacitance and load change, which affects the input transition time. That’s why we use delay tables with axes for input transition and output load to more accurately calculate the delay for each cell

### Delay table usage Part 1

* Basically all gates will have their own delay table.

<img width="1337" height="659" alt="image" src="https://github.com/user-attachments/assets/dddf1f73-8325-4127-9377-7ec909935177" />

### Delay table usage Part 2

<img width="1460" height="680" alt="image" src="https://github.com/user-attachments/assets/3e2778c6-59ba-44d1-85c4-7268bcd8ce80" />

If both buffers have the same input and load, there's no skew. Unequal values cause skew hich can basically break timing in big circuits

* Skew = difference in clock arrival time
* Slew = how fast voltage changes
* Latency = clock delay
* CTS builds the clock network to keep everything in sync.

### Lab steps to configure synthesis settings to fix slack and include vsdinv


