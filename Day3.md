# VSDIAT SKY130 Day 3: Design Library Cell Using Magic Layout and ngspice characterisation

## Labs for CMOS Inverter NGSPICE Simulations

### IO Placer Revision

* We can change the pin configuration as well.

* Below is the content inside floorplan.tcl

<img width="1864" height="850" alt="image" src="https://github.com/user-attachments/assets/6d2070c9-bff1-4ac0-8717-a497de789576" />

* We copy "::env(FP_IO_MODE) 1" variable from the floorplan.tcl file to change pin configuration
* We then run floorplan again:

<img width="987" height="329" alt="image" src="https://github.com/user-attachments/assets/0916bc77-63b2-4228-a155-9afec180d044" />

### SPICE deck creation for CMOS inverter

<img width="1070" height="500" alt="image" src="https://github.com/user-attachments/assets/f38ad108-59be-45a3-a9a4-83c46cdbb405" />

### SPICE Simulation Lab for CMOS Inverter

* To run the **SPICE** simulation, We begin by opening the **NGSPICE simulator** and sourcing the circuit file using the source command. Once the file is loaded, we execute the simulation with the **run** command. After that, we use the **setplot command** to select the appropriate simulation type defined in the SPICE deck. To explore the results, we type display to view the list of available nodes, and finally, we plot the desired output, for example, using plot out vs in to visualize the output signal relative to the input

* Circuit file:

<img width="778" height="543" alt="image" src="https://github.com/user-attachments/assets/d25d910c-b7d7-4438-96e1-520696784286" />

Difference between the two waveforms:

<img width="1108" height="528" alt="image" src="https://github.com/user-attachments/assets/2962b63b-fbd0-45d8-99f0-1c6218004aac" />

### Switching Threshhold Vm

* The switching threshold is the moment when the input and output voltages are the same, and both the PMOS and NMOS transistors are turned on. When this happens, current can flow directly from the power supply (VDD) to ground (GND), which isn't supposed to happen. This causes what's called a short-circuit current, leading to power loss and possible overheating in the chip.

**Vin = Vout**

<img width="1028" height="524" alt="image" src="https://github.com/user-attachments/assets/dd9bbc3c-afa7-45a7-a6f0-2eecb3a9651c" />

<img width="945" height="475" alt="image" src="https://github.com/user-attachments/assets/dbdcf0ec-02b9-40d4-89a7-55ab38008fad" />

### Static and Dynamic Simulation of CMOS Inverter

* The input is essentially the pulse and hence, we will perform a **transient analysis.**

<img width="994" height="564" alt="image" src="https://github.com/user-attachments/assets/3586472b-0b1f-4dc2-8786-4814e7cdce10" />

### Lab Steps to git clone vsd std cell design

**Github Repo Link:** [https://github.com/nickson-jose/vsdstdcelldesign](url)
* We have to copy the link witin the repo, which is- [https://github.com/nickson-jose/vsdstdcelldesign.git](url)

* As we can see below, The files have been successfully downloaded :

<img width="1539" height="527" alt="image" src="https://github.com/user-attachments/assets/5bf1fa97-fad6-4799-becf-46aea96a3080" />

* After copying the sky130A.tech file to the vsdstdcelldesign dir :-
* We can then open the layout using magic, using the command: magic -T sky130A.tech sky130_inv.mag &

As we can see, It should look like this:

<img width="1870" height="895" alt="image" src="https://github.com/user-attachments/assets/715c84aa-0915-444b-b008-bd6a8d4ff505" />

## Inception of layout -- CMOS fabrication process
### Create Active regions

**16-mask CMOS process**

1) Selecting a substrate

* Called the **P type Substrate(P-Substrate)**

<img width="1831" height="669" alt="image" src="https://github.com/user-attachments/assets/993cc342-9ff9-49c9-87b0-b184e79ef036" />

2) Creating active region for transistors

* We begin by creating specific areas on the chip where the transistors will go. To make sure these areas stay isolated from each other, we first grow a 40nm layer of silicon dioxide, followed by an 80nm layer of silicon nitride. Then, we coat the surface with a light-sensitive material called photoresist. A mask is placed on top to protect the regions where the transistors will be. When UV light is applied, it removes the unprotected parts of the photoresist. After that, we remove the mask and leftover photoresist. The chip is then placed in a furnace so that oxide grows in the exposed areas, creating isolation. Finally, we use hot phosphoric acid to remove the silicon nitride, leaving only the silicon dioxide and the base silicon layer.


