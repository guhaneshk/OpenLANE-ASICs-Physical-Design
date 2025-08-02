# VSDIAT SKY130 DAY 4 : Pre-Layout Timing Analysis and Importance of Good Clock Tree

## Timing Modelling Using Delay Tables

### Lab Steps To Convert Grid Info Into Track Info

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

* I did not have any violations and hence I did not perform any of it.
* But to fix violations, we have to look at the current value of SYNTH_STRATEGY, SYNTH_BUFFERING, SYNTH_SIZING, and SYNTH_DRIVING_CELL.

Now, we run floorplan,

<img width="1790" height="484" alt="image" src="https://github.com/user-attachments/assets/206bb500-b2f1-4905-9be0-8579c17c97c0" />

As we can see, my floorplan failed

To fix this I ran these commands one by one, 
* init_floorplan
* place_io
* global_placement_or
* detailed_placement
* tap_decap_or
* detailed_placement

As we can see the placement file has been created:

<img width="1304" height="330" alt="image" src="https://github.com/user-attachments/assets/20b09be3-541a-4b75-9610-94aaf4ecea39" />

After running magic using the command, *magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def*  ,We can see the placement:

<img width="1841" height="620" alt="image" src="https://github.com/user-attachments/assets/eaf1120b-77e8-4a00-9fe2-fd3d17ddf440" />

<img width="1626" height="791" alt="image" src="https://github.com/user-attachments/assets/d61b9c3d-f717-4e60-9d1b-f66d0834a8bf" />

As we can see below I found our cell:

<img width="357" height="403" alt="image" src="https://github.com/user-attachments/assets/5ce1a79c-7ef7-4a31-9ec2-e1b4634b9f3f" />


## Timing analysis with ideal clocks using openSTA

### Setup timing analysis and introduction to flip-flop setup time

Clock analysis using a single clock.

<img width="1226" height="674" alt="image" src="https://github.com/user-attachments/assets/e12c5561-cbd8-4f60-b880-cb37f6e0a844" />

<img width="1399" height="670" alt="image" src="https://github.com/user-attachments/assets/ae0ebf2b-f2da-47a8-9823-74361c82d300" />

### Introduction to clock jitter and uncertainty

<img width="1194" height="676" alt="image" src="https://github.com/user-attachments/assets/104176a1-417b-4af1-b8e3-f2a3dc78b7cd" />

* we model jitter mainly for uncertainity.

* Detailed circuit:

<img width="1418" height="673" alt="image" src="https://github.com/user-attachments/assets/1bb8caa3-a8db-4204-836f-7269b900bbd8" />

### Lab steps to configure open STA for post synth timing analysis

* we first create a pre_sta.conf file and a my_base.sdc file.

<img width="1130" height="364" alt="image" src="https://github.com/user-attachments/assets/b2acca57-388f-4300-8a7b-53fde3ec803e" />

* We finally run sta pre_sta.conf and check its timing

### lab steps to optimize synthesis to reduce setup violations

* Since it concluded with a violation- we have to fix it.
* If fanout is high, go back to OpenLane and set:
*set ::env(SYNTH_MAX_FANOUT) 4*
Then re run synthesis. This helps limit the number of loads per net, reducing delay and improving slack.

<img width="380" height="79" alt="image" src="https://github.com/user-attachments/assets/9bc0bf94-65ba-4502-b3ab-e11c4221b653" />

* With this we can get an expected value for the slack.

### Lab steps to do basic timing ECO

* To reduce slack violations further, we can upsize cells with high fanout, this gives stronger drivers to handle large capacitive loads which cuts delay. Since we can't tweak the load directly, increasing cell size helps.
* even the tns are improved.

## Clock tree synthesis TritonCTS and signal integrity

### Clock tree routing and buffering using H-Tree algorithm

<img width="1555" height="667" alt="image" src="https://github.com/user-attachments/assets/6c82b924-f76e-4ee5-a14b-d0ad43ec69a2" />

* t2-t1 = skew
<img width="1357" height="617" alt="image" src="https://github.com/user-attachments/assets/f85e30da-d4f7-464d-a083-b3b518bdecda" />

<img width="1023" height="604" alt="image" src="https://github.com/user-attachments/assets/b2b95fcb-d3d2-46e7-95a6-0b1f249b0cd5" />


* A clock tree basically distributes the clock signal to all flip flops with minimal skew which means minimal difference in arrival times. Skew is caused by unequal wire lengths, delays, or routing. To reduce this, H-tree routing is used, which places the clock source at the center and evenly splits it to keep delays balanced. Buffers are added to preserve signal quality. Unlike data buffers, clock buffers maintain equal rise and fall times for consistent timing across the circuit.

* As you can see, we added a bunch of buffers here:

<img width="1000" height="612" alt="image" src="https://github.com/user-attachments/assets/49f8eb62-9db5-492d-8627-e1866c98a1eb" />

### Crosstalk and clock net shielding

Clock nets are basically highly sensitive and need shielding to avoid crosstalk when signals on nearby wires interfere due to high coupling capacitance. This interference causes two main problems, which are:
* Glitch: Voltage dips or spikes that corrupts data
* Delta delay: Extra delay when both wires switch at once, increasing the clock skew

To avoid this, shielding wires tied to power/ground are placed on either side of critical nets like clock lines, isolating them from interference and improving the overall timing.

<img width="902" height="647" alt="image" src="https://github.com/user-attachments/assets/a14101cb-e144-4a2b-aa86-d0b8d285498c" />


<img width="664" height="459" alt="image" src="https://github.com/user-attachments/assets/a32fb075-4352-418e-9c52-119677c79f70" />


<img width="1359" height="655" alt="image" src="https://github.com/user-attachments/assets/db6d21f0-5558-4de8-8af8-405046be4c7a" />

### Lab steps to run CTS using TritonCTS

* We have to change/switch the cells above 1 which are cauing slack violations, this causes the time to lessen overall.

<img width="626" height="93" alt="image" src="https://github.com/user-attachments/assets/4c108756-3ceb-4366-93cd-e2d73f153825" />

* After this we need to update our results since we did some chnges in the cells.
* after finishing write_verilog, we run floorplan finally.

* Finally we run CTS, with the command *run_cts*

<img width="1130" height="157" alt="image" src="https://github.com/user-attachments/assets/5d5d87e4-d38b-4888-8c5f-e5be6e3e1384" />

### Lab steps to verify CTS runs

* The TCL Commands can be found in */Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands* 

Whats actually happening/content inside the *cts.tcl* file
* This is the file that acutally controls the CTS Logic
* This file includes various variables like *CTS_CLK_BUFFER_LIST*, which are buffers used to branch the clock tree; *CTS_ROOT_BUFFER*, which is the  biggest buffer and *CTS_MAX_CAP* which is the capacitance limit at the output to avoid delays.

## Timing Analysis with real clocks Using OpenSTA

### Setup timing analysis using real clocks

* At this point, the clock has been successfully built.

<img width="1038" height="660" alt="image" src="https://github.com/user-attachments/assets/c6aec952-1076-49c5-8220-3e4ee5c96c82" />


<img width="1412" height="663" alt="image" src="https://github.com/user-attachments/assets/03a755d1-5540-45f4-bcc7-3ebc817bbe22" />

* Slack = Data required time – Data arrival time, we want slack to be zero or positive for timing to meet
* Hold time checks that data is held stable long enough after the clock edge and violations happen if buffers cause signals to arrive too early

### Hold timing analysis using real clocks

<img width="1291" height="660" alt="image" src="https://github.com/user-attachments/assets/f2f41fcf-76ba-45d4-8231-3829ef8e4826" />


<img width="1480" height="689" alt="image" src="https://github.com/user-attachments/assets/a9266fee-6aaf-4018-9e61-cbca3bfe8753" />

* Hold analysis uses the same clock edge for both launch and capture, the formula is lack = data arrival time – data required time, and it should be ≥ 0

* Hold violations happen when the path is too fast, due to low combinational delay, clock skew (delta1/delta2), or basically small hold time

### Lab steps to analyze timing with real clocks using OpenSTA

* We start off with opening openroad and then we create the db file using the read_lef command.
* We read led with: *read_lef /openLANE_flow/designs/picorv32a/runs/17-07_00-07/tmp/merged.lef*
We then make a db file: * write_db pico_cts.db*
* We read def with: *read_def /openLANE_flow/designs/picorv32a/runs/17-07_00-07/results/cts/picorv32a.cts.def*
<img width="1156" height="102" alt="image" src="https://github.com/user-attachments/assets/9db379de-fbef-463e-9f89-88d07d832fa7" />

First, it loads the timing libraries which are the slowest (LIB_SLOWEST) and fastest (LIB_FASTEST) for the worst/best case delay analysis.
* Then we read in the .sdc file, Verilog netlist, and database, This basically sets the timing environment
* We use this command, *set_propagated_clock [all_clocks]* to enable actual clock delar
We finally run *report_checks* to view or hold the slack. Also touting later affects hold slack due to added RC delays

### Lab steps to execute OpenSTA with right timing libraries and CTS assignment

* TritonCTS only works with typical corner timing, so using min.max results isn’t really valid here
To fix that, we close OpenROAD, reopen it, and reload everything — but this time using the typical timing library.
We re-link the design, bring in the clock and SDC file again, and then run a fresh timing report.
* To read the sdc we use link_design picorv32a
For the report, we typr in *report_checks -path_delay min_max -fields {slew trans net cap input_pin} -format full_clock_expanded -digits 4*

If setup slack still looks off, we can tweak the clock buffer list (like removing the first one) to help TritonCTS optimize better.

But as you can that the hold slack is met:

<img width="382" height="40" alt="image" src="https://github.com/user-attachments/assets/98813316-dcab-477f-81d6-345853e0b0f9" />

Likewise, even the setup slack was met.

### Lab steps to observe impact of bigger CTS buffers on setup and hold timing

We get some errors because the current DEF file is from after CTS
* To fix this, we load the DEF from placement instead 

<img width="1162" height="51" alt="image" src="https://github.com/user-attachments/assets/a96610cd-64ab-4cb7-acb9-c3c24ac19c04" />

After switching to the placement DEF, we re run CTS and it completes successfully.

After this, back in OpenROAD, we save a new .db file (like : pico_cts1.db) just like before

Then, we re read the Verilog, LIB_SYNTH_COMPLETE, link the design, read the SDC, set propagated clocks, and finally run timing checks

We observe the new hold(which was violated again sadly)

We can also check clock skew using : *report_clock_skew*

To fiunally re-add the buffer that was removed, we ened to exit OpenROAD and run this command: *set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]*

<img width="1155" height="73" alt="image" src="https://github.com/user-attachments/assets/f742769c-5ba5-4cef-8cea-5cb842260cae" />


—---------------------------------------**END OF DAY 4**\--------------------------------------------------


