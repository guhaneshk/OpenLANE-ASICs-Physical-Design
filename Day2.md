# SKY130 Day 2: Good vs Bad Floorplan and Introduction to Library Cells

## Chip Floor Planning Considerations
### Utilization factor and aspect ratio

* Net list- A netlist basically defines the connectivty between all the components; example below:
<img width="1004" height="587" alt="image" src="https://github.com/user-attachments/assets/f6f2326a-e47a-479a-a269-988a0cdf1867" />

* When defining the deminions of the chip, we are mosltly dependent on the **logic gates.**
* Utilization Factor: **(Area Occupied by Netlist)/(Total Area of the Core)**

* Aspect Ratio : Height/ Width

### Utilization factor and aspect rat

*Pre placed cells can be divided into blocks and still perform the same intended taks, but the thing is- pre placced cells should be really well designed because they are essentially complex logic gates that can be reused.
Image down below:
<img width="1026" height="558" alt="image" src="https://github.com/user-attachments/assets/592a008a-bc57-4f92-9c89-96e272612b93" />

We essentially do this by **extending** the **IO Pins**:

<img width="532" height="225" alt="image" src="https://github.com/user-attachments/assets/d087bb74-eff3-4530-8c0f-53a8c81845ab" />

* As we can see we split the two blocks into two seperate IP's or modules:

<img width="823" height="374" alt="image" src="https://github.com/user-attachments/assets/3053a4df-ed07-452c-a9b6-4d22dfafdec3" />

**Other IP's such as memory, clock-gating cells, etc**

 * The arrangement of these IP's in a chip is called as **Floorplanning**.
 * **Automated Placement**

### De-coupling capacitors

* **Pre-Placed Cells** should be placed in such a way that- after placing it, It **cannot be moved afterward.**
* We have to surround these pre-placed cells with **Decoupling Capacitors.**

<img width="970" height="527" alt="image" src="https://github.com/user-attachments/assets/326f9966-0f5b-42aa-b282-066f399ee6d9" />

* De-coupling capacitors are filled with charges and it matchhes the voltage of the power supply as well.
* The amount of current that respective circuit needs for changing logic is provided by the de-coupling capacitors.
* When there's no switching happening, the De-coupling capacitor replenshes its current within the free time.

### Power Planning
<img width="854" height="507" alt="image" src="https://github.com/user-attachments/assets/fa1ed3bc-b24a-4b0b-b086-306cda8a4c28" />

* The **inverter** **dicharges** all the logic 1's to logic 0 and vice versa- and all logic 0's will **charge** to logic 1.

This is what happens:

<img width="786" height="269" alt="image" src="https://github.com/user-attachments/assets/565cc9af-b5ec-42c6-b947-2209b203c2b3" />

* Best way to solve this problem is to add more power supplies all around:

<img width="857" height="578" alt="image" src="https://github.com/user-attachments/assets/bd73c56d-94c4-4215-839f-984f5e4959c1" />

**Better version**: 

<img width="1022" height="579" alt="image" src="https://github.com/user-attachments/assets/63b559e4-cd94-4b0d-9cae-a8a6edef57d3" />

### Pin placement and logical cell placement blockage

* **Complete design:**
<img width="705" height="573" alt="image" src="https://github.com/user-attachments/assets/08470e68-dae7-4abf-8c94-13d395d350ab" />

* The connectivity information between the gates is verilog and is called as the **"Netlist"**.

**Pin placement and logical cell placement blockage:**
<img width="967" height="566" alt="image" src="https://github.com/user-attachments/assets/0b8f2b04-c4c8-4252-b1c6-5bb2c2c6df05" />

### Steps to run floorplan using OPENLANE

* The content inside the README file under the configurations dir:
<img width="1909" height="902" alt="image" src="https://github.com/user-attachments/assets/191edc3c-5696-4b5d-82ba-5db8d1bec068" />

* Specifically for **floorplanning:**
<img width="1842" height="841" alt="image" src="https://github.com/user-attachments/assets/f1f73c6c-6c03-4d6e-8dd0-7a93848af97a" />

* Config.tcl file:
<img width="1278" height="448" alt="image" src="https://github.com/user-attachments/assets/54a5e525-2152-4ac6-a5b2-930018f01c14" />

* After running floorplan:
<img width="1869" height="844" alt="image" src="https://github.com/user-attachments/assets/453ca2b7-3a26-4e6c-8c68-bff43a7cc2de" />

### Review floorplan files and steps to view floorplan

* We can use our floorplan results to calculate our DIE
* Floorplan results:
 <img width="1857" height="903" alt="image" src="https://github.com/user-attachments/assets/c23869d5-1031-408e-8195-5a49dc476ccc" />

**FLOORPLAN:**
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/43170bae-1d40-4c53-8ef9-ffd3436c689a" />

The command is : magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

### Review floorplan layout in Magic

* We click left mouse click and right mouse click which creates a block and parallely pressing Z, zooms that specific part in.

<img width="1634" height="819" alt="image" src="https://github.com/user-attachments/assets/4308340d-a0f4-4942-9e56-89f6fe6d93cf" />

<img width="1061" height="433" alt="image" src="https://github.com/user-attachments/assets/65dabf18-24d4-4adc-a59a-5d31e5f3236a" />

Full image:

<img width="1919" height="961" alt="image" src="https://github.com/user-attachments/assets/ddcee1ea-0306-464a-8022-4e854bc72374" />

## Library Binding and Placement
### Netlist binding and initial place design

<img width="1004" height="571" alt="image" src="https://github.com/user-attachments/assets/8bb329d1-c042-4fde-ae96-ea87d0e87368" />

* The library will have the height and widht of every cell as well as its delay information.

<img width="309" height="387" alt="image" src="https://github.com/user-attachments/assets/e7a67984-3a87-4a31-9074-d7d9ed33970c" />

* The more bigger the AND Gate in size = less resistance = more faster.

### Optimize placement using estimated wire-length and capacitance

* **Placement**:

**1st logic:**

<img width="1078" height="251" alt="image" src="https://github.com/user-attachments/assets/5c1b031c-5eca-44c2-bbdb-dcfd6d8fd8a1" />

**2nd Logic:**

<img width="1062" height="475" alt="image" src="https://github.com/user-attachments/assets/66eb5d28-9833-47d7-96b5-c0e322320430" />

### Final placement optimization

**3rd Logic:**

<img width="1038" height="485" alt="image" src="https://github.com/user-attachments/assets/4f5ed8ee-0497-4f09-9b80-20d938ee4d93" />

**4th Logic:**

<img width="1053" height="529" alt="image" src="https://github.com/user-attachments/assets/1a65a761-2ea2-432c-9e44-f960ef1ee780" />

### Need for libraries and characterization

**Lib characterization and Modelling:**

<img width="1027" height="578" alt="image" src="https://github.com/user-attachments/assets/edd68673-a553-4341-9c36-120384206e8a" />

### Congestion aware placement using RePlAce

**When running placement (run_placement) in Openlane, These functions occur:**
* **Global Placement:** Reduces wire length
* Optimization and detailed placement

* We can look at it in the placement dir under results in MAGIC by typing in: magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

<img width="1202" height="809" alt="image" src="https://github.com/user-attachments/assets/ce0b4ed4-c7b4-4a77-8734-6e69885bfcfd" />

As we can see the amount of standard cells above

* Zoomed in:

<img width="1378" height="779" alt="image" src="https://github.com/user-attachments/assets/c8d0d1ac-e27b-43e5-b828-a3f180c9ebfa" />

## Cell Design and Characterisation Flows

### Inputs for cell design flow

**The cell design flow is divded into three steps:**
* Inputs
* Design Steps
* Outputs
  
### Circuit design step

<img width="1141" height="676" alt="image" src="https://github.com/user-attachments/assets/32ffd0cf-1911-4ef4-86a0-b339018fe73c" />

### Layout design step

<img width="609" height="392" alt="image" src="https://github.com/user-attachments/assets/28d973a0-029d-4d63-9b83-e801a17c595c" />

<img width="360" height="517" alt="image" src="https://github.com/user-attachments/assets/377babb6-3aa4-4523-a0c1-56348acd2b0c" />

### Typical characterization flow

**FLOW:**

<img width="920" height="491" alt="image" src="https://github.com/user-attachments/assets/f0ee11a6-5cac-41aa-8080-76a57e2e3d20" />

Charactarization software named **GUNA**

<img width="1002" height="541" alt="image" src="https://github.com/user-attachments/assets/ed32627c-04d3-4dc7-9aba-4c149990b36c" />

## General Timing Characterisation Parameters

### Timing threshold definitions

<img width="980" height="584" alt="image" src="https://github.com/user-attachments/assets/b34c6138-4486-4ebb-9333-7f20b15b5ee8" />

<img width="488" height="484" alt="image" src="https://github.com/user-attachments/assets/1172ff89-2bc9-4ce7-9ff5-895ffe76c500" />

<img width="487" height="491" alt="image" src="https://github.com/user-attachments/assets/72b0f701-877d-4054-bc0b-dc754df32003" />

### Propagation delay and transition time

**Propoation delay formula:** time(out_x_thr) - (time_x_thr)
<img width="258" height="71" alt="image" src="https://github.com/user-attachments/assets/9f907a0b-95be-44df-9724-a186b1814318" />

**Transition time forumla:** time(slew_high_x_thr) - time(slew_low_x_thr)
<img width="815" height="370" alt="image" src="https://github.com/user-attachments/assets/79c299c1-9eb5-4cad-9444-256c25a0967a" />

<img width="411" height="79" alt="image" src="https://github.com/user-attachments/assets/7c968c7e-2ae7-48a6-a09a-fab1d73bfa92" />

<img width="1035" height="520" alt="image" src="https://github.com/user-attachments/assets/ce2207da-1813-4c03-8060-45b60b059912" />


—---------------------------------------**END OF DAY 2**\--------------------------------------------------


