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

<img width="1602" height="665" alt="image" src="https://github.com/user-attachments/assets/395fa83e-d069-4df5-b950-baf60048d558" />

<img width="1304" height="594" alt="image" src="https://github.com/user-attachments/assets/d99096e8-b9e1-443b-ac51-d826ac22a65e" />

### Formation of N-well and P-well

* Mask 2 protects the N Well area while the P-Well is formed, and Mask 3 does the reverse. UV light removes the exposed photoresist, leaving only the protected areas
* The wafer is then placed in a furnace, where boron is diffused to create the P-Well and phosphorus for the N Well. This forms the separate regions for NMOS and PMOS transistors on the same chip. (also known as twintub process)

<img width="1439" height="689" alt="image" src="https://github.com/user-attachments/assets/4a12d58e-ba03-4fc2-bab0-fff7fa973286" />

### Formation of gate terminal

* The gate is essentially where you control your **threshhold voltage** (Turning on of our transistors)

The image below includes the formula for the same as well:

<img width="1414" height="682" alt="image" src="https://github.com/user-attachments/assets/dacbff2b-e0c2-4767-8336-a1cdc8cde466" />

* First a photoresist layer is applied to the wafer to mark the regions that need protection and then it is followed by mask 4. UV light is then used to remove the exposed photoresist, then low energy boron is implanted into the P-Well using Mask 4 to adjust the threshold voltage. Likewise, phosphorus or arsenic is implanted into the N-Well with Mask 5. The oxide layer which was damaged during implantation, is removed using hydrofluoric acid and replaced with a high quality silicon dioxide layer. A polysilicon film is added next and Mask 6 is used to define and etch the gate terminal using photolithography.

<img width="1339" height="624" alt="image" src="https://github.com/user-attachments/assets/3de630ce-c83d-42ef-b67c-e27b4d925849" />

### Lightly doped drain (LDD) formation

* Lightly Doped Drain are added to prevent two big issues as devices shrink which are the hot electron effect (where high energy electrons damage Si–Si bonds or leak into oxide layers) and the short channel effect (where the drain’s electric field interferes with gate control). To form LDDs, light doping (N⁻ for NMOS, P⁻ for PMOS) is done using Masks 7 and 8. Then, oxide spacers are added via anisotropic etching to protect these regions before heavier doping (N⁺/P⁺) forms the actual source and drain.

<img width="1291" height="630" alt="image" src="https://github.com/user-attachments/assets/cc65d2dd-627d-4b8a-85b8-be0500387e2c" />

### Source – drain formation

* To make the source and drain regions in a CMOS chip, we first add a super thin oxide layer to stop the dopants from sinking too deep (this is called preventing channeling). Then we use Mask 9 to implant N+ (using arsenic) into the P well and Mask 10 to implant P+ (using boron) into the N well. Little sidewall spacers help keep the earlier dopings safe. In the end, we increase the heat in the furnace so everything settles properly into place

<img width="1354" height="622" alt="image" src="https://github.com/user-attachments/assets/c309727f-5fb3-4703-baca-b8cbda2711e3" />

### Local interconnect formation

* We first clear off the thin oxide layer to open up the gate, source, and drain. Then, we coat the surface with titanium which reacts under heat to form materials that help electricity flow better TiSi2 for low resistance and TiN for short connections. After that, we use Mask 11 and a special cleaning process, RCA to get rid of any extra titanium.

<img width="1464" height="677" alt="image" src="https://github.com/user-attachments/assets/d58d834f-dc4f-4bca-b6d7-4786dfc180ee" />

### Higher level metal formation

* So the earlier TiN layer was kinda bumpy, which isn’t good, so to fix that, we add a layer of doped silicon dioxide which helps with temperature and blocking sodium. Then they smooth everything out using CMP, basically sanding it flat and After that, they drill tiny holes with photolithography (Mask 12), add a thin TiN layer, fill it with tungsten and polish it again.
* Then after that we add the metal layers, rhey add aluminum (Mask 13), clean off extra, repeat the process with new holes (Mask 14), and add another aluminum layer (Mask 15). Finally, they finsish it with silicon nitride and use Mask 16 to open the final points.

<img width="1174" height="682" alt="image" src="https://github.com/user-attachments/assets/357470b8-5141-4990-a1f8-c17206fd54d1" />

### Lab introduction to Sky130 basic layers layout and LEF using inverter

<img width="1614" height="781" alt="image" src="https://github.com/user-attachments/assets/6436398c-e62b-49ee-965d-60b7adba3102" />

* As you can see above, we can choose layers from the color pallete in the right side.

* For selecting a particular part and to check its connectivity, we press S- Three times.

<img width="1742" height="924" alt="image" src="https://github.com/user-attachments/assets/d0962f80-966f-4c4b-badc-892421cbe83c" />

### Lab Steps to Create STD Cell Layout and Extract SPICE Netlist

* We first create a B Box

<img width="578" height="409" alt="image" src="https://github.com/user-attachments/assets/8413264c-99cc-4753-986e-3965d453f502" />

<img width="694" height="436" alt="image" src="https://github.com/user-attachments/assets/89663bbd-9276-4174-b7a9-b2c3a8c21aa1" />

* We can use the DRC Dropdown to find violations/errors

* Extracting:

<img width="1120" height="428" alt="image" src="https://github.com/user-attachments/assets/c5312e4d-4c75-414d-8f42-f77785a901b8" />

<img width="819" height="186" alt="image" src="https://github.com/user-attachments/assets/f39399f6-4921-4566-9a8b-27bab916e079" />

* As we can see below it created the new file, *sky130_inv.spice* :

<img width="954" height="305" alt="image" src="https://github.com/user-attachments/assets/e1547f8e-2a7d-4826-9bac-fc9ed501ae3f" />

## SKY130 Tech File Labs

### Lab Steps To Create Final SPICE deck using SKY130 tech

<img width="1123" height="516" alt="image" src="https://github.com/user-attachments/assets/bc65e182-09b0-4279-87dc-10f841ae66ec" />

<img width="1058" height="540" alt="image" src="https://github.com/user-attachments/assets/fc02b495-cea9-4949-b371-df82ae98873a" />

<img width="1390" height="769" alt="image" src="https://github.com/user-attachments/assets/5e775acd-4b52-4e55-b537-e2dea21679cd" />

### Lab steps to characterize inverter using sky130 model files

* We can type in ngspice sky130A_inv.spice, to load the spice file in NGSPICE:

<img width="1357" height="698" alt="image" src="https://github.com/user-attachments/assets/6603149e-7ba9-4699-b3ea-5f8dc9b63f4f" />

<img width="1900" height="1044" alt="image" src="https://github.com/user-attachments/assets/4b31ca23-8a01-4cb5-b9e5-6b930c5e4ec3" />
* We changed C3 because its value was too low and it caused spikes in the graph>

<img width="1171" height="779" alt="image" src="https://github.com/user-attachments/assets/1551cb5c-0aa6-4687-b0dc-c5750ef08f3a" />

* The Y Axis is the voltage.

### Lab introduction to Magic tool options and DRC rules
* Link/Resource on how magic performs DRC: [http://opencircuitdesign.com/magic/](url)
    * This website has a lot of tutorials and guides on Magic.

### Lab introduction to Sky130 pdk's and steps to download labs


