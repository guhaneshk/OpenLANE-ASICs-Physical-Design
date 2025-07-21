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


