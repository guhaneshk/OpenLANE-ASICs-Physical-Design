# VSDIAT SKY130 DAY 5 : Final Steps For RTL2GDS Using TritonRoute and OpenSTA

## Routing and design rule check (DRC)

### Introduction to Maze Routing – Lee’s algorithm

<img width="1507" height="649" alt="image" src="https://github.com/user-attachments/assets/630af9eb-133c-4371-acc9-2cfd3fd2a78c" />

* Lee is a famous person who invented the maze routing/lee's algorithm concept.

<img width="493" height="297" alt="image" src="https://github.com/user-attachments/assets/effc2ea7-c72f-4f4e-bdc6-3ada6baf85f4" />

* Maze routing , like solving a grid maze basically connects two points ,source → target,with the shortest possible path, often L-shaped and with minimal zigzags
* We mark obstacles, source (S), and target (T).

<img width="445" height="247" alt="image" src="https://github.com/user-attachments/assets/80ee1b62-4a29-4621-b61a-4fa5c7941e0d" />

* Starting from S, adjacent cells are labeled 1, then the wave spreads outward: 2, 3, 4, etc, until it hits T.

### Lee’s Algorithm conclusion

<img width="786" height="395" alt="image" src="https://github.com/user-attachments/assets/48357126-a72f-4829-a221-ab23499ad23c" />

* Lees algorithm expands cell values to find a path and then backtracks from the target to the source, selecting the shortest route with the fewest bends.

### Design Rule Check

There is 3 typical rules:

<img width="802" height="403" alt="image" src="https://github.com/user-attachments/assets/3567c849-f90e-4589-9dfc-e92385b5f0b7" />

* The wire should be atleast that much for photolithography to work.

<img width="608" height="389" alt="image" src="https://github.com/user-attachments/assets/3d3f21cb-5f0e-4bb0-994e-cb3a5a06b0c2" />

* Pitch is basically the center to centre distance between features to achieve the highest print resolution.

<img width="564" height="313" alt="image" src="https://github.com/user-attachments/assets/efe27be4-1e21-4764-a8ac-61a18c84d49f" />

* Wire spacing is the minimun spacing between wires.


2 New rule designs to be checked:

<img width="476" height="374" alt="image" src="https://github.com/user-attachments/assets/2a9716b1-1b90-4043-8fc3-019fd45433b8" />

<img width="501" height="398" alt="image" src="https://github.com/user-attachments/assets/5a74c11d-287a-4fa0-8af6-9853a6272c39" />

## Power distribution network and routing

### Lab steps to build power distribution network

To start off, just run docker a usual but this time, we put prep -design picorv32a -tag (date) to get back.

* We then type  echo $::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/results/cts/picorv32a.cts.def
* then we generate the power distribution network using the command, *gen_pdn*.

Then it should be successfull:

<img width="815" height="37" alt="image" src="https://github.com/user-attachments/assets/0e9cb6cd-4d69-4144-8b28-20749c853b48" />

### Lab Steps From Power Straps To STD Cell Power

<img width="780" height="511" alt="image" src="https://github.com/user-attachments/assets/5a9e3382-d052-418f-92ec-c74e76010000" />

The diagram above shows power (red) and ground (blue) boxes arranged in rings with corner pads, vertical stripes connected by vias, and standard cells placed in rows, where power straps feed the rails and macros

Our next step is routing, and our current def has been updated.

### Basics of global and detail routing and configure TritonRoute

* We first run routing with this command: *run_routing* . After routing, **tritonroute** is used.

Routing is divided into two main steps:
* **Global Route:** It is also known as fast route, It is the step where the chip layout is split into tiles or rectangles to sketch rough paths for signals.
* **Detail route:** follows the plan closely, using algorithms and the route guide to find the best, most rule ompliant connections between components.

<img width="1225" height="635" alt="image" src="https://github.com/user-attachments/assets/86eff64f-6590-4662-998a-c419618d9b97" />

  
