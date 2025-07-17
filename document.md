# Introduction to QFN-48 Package, chip, pads, core, die and IPs 

- Arduino's main chip/processor - Block Diagram
![chunk-0-img-0.jpeg](chunk-0-img-0.jpeg)
- Integrated circuit(IC)(Arudiono) / Package

The name of the chip: QFN - 48 package (Quad Flat No-Leads).
![chunk-0-img-1.jpeg](chunk-0-img-1.jpeg)
$7 \mathrm{mmx} 7 \mathrm{~mm}$
This picture shows how the chip is connected to the package via wire bonds.

- Pads: This is where signals go inside and outside of the chip.
- Core: The place where the digital logic sits like the AND,NOR,XNOR,Etc gates.
- Die: Is basically the piece where it contains a proper constructed IC inside. (the outer)
![chunk-0-img-2.jpeg](chunk-0-img-2.jpeg)

Foundry- A big factory containing machines that manufacture chips (deposition systems).

Foundry IPs are pre designed, silicon hardware blocks (like PLLs or SRAM) provided by chip factories to save design time, while macros are pre-built digital logic blocks (like SPI controllers) for common functions that can be customized before integration. Both are plug and play components for chip designers, but IPs are physical/analog with fixed layouts, whereas macros are digital and often configurable

# Introduction to RISC-V 

Basic process: Risc V Assembled language program is then converted into machine learning programs (binary 0 s and 1 s ) and then finally these bits get executed to the hardware layout.

The image down below is the schematic of the process:

![chunk-0-img-3.jpeg](chunk-0-img-3.jpeg)

# From Software Applications to Hardware 

- System software converts the applications to binary for the hardware to make it executable.
- Main components include: The OS, Compiler and the Assembler.
- OS Converts into respective assembling language binary programs. It also handles IO operations, memory allocation, etc.
- The compiler translates code like C ++ , java, etc into architecture specific machine instructions (ISA) like x86/ARM/RISC-V, generating executable (.exe) files for the assembler.
- The assembler basically converts the instructions into binary for the hardware.

The simplified process is shown below:

![chunk-0-img-4.jpeg](chunk-0-img-4.jpeg)

# SoC design and OpenLANE 

## Introduction to all components of open-source digital asic design

Three main components for Asics include:

- RTL IP's
- EDA Tools- Qflow, OpenRoad, OpenLane
- PDK Data
-PDK(Process design Kit) is the interface between the FAB and the designers. Basically a collection of multiple files used to model the fabrication process.(foundry) -RTL IPs- These are already predesigned, reusable hardware blocks and these blocks essentially use complex logic to describe the functioning of the circuit. -EDA Tools- Used for design, analysing and simulating circuit designs. Examples are Qflow, open road, etc.

![chunk-0-img-5.jpeg](chunk-0-img-5.jpeg)

# 130nm processor example: 

- Intel P4EE @3.46 GHz - 2014

Asic Flow objective : RTL to GDSII
Simplified RTL2GDS flow
Simplified schematic:
![chunk-0-img-6.jpeg](chunk-0-img-6.jpeg)

Synthesis: Converts RTL to a circuit out of components from the standard cell library(SCL)
![chunk-0-img-7.jpeg](chunk-0-img-7.jpeg)

Each standard cells have regular layout
Chip floor planning: Partition the chip die between different system building blocks and placing their IO pads.

- Macro-Floor planning: Dimensions, pin locations, rows, etc.


# (Just noticed that I don't have to document videos and I spent too much time doing this lol) 

## Eda Tools

## OpenLANE Directory structure in detail

- Getting into the openlane working directory on linux:
![chunk-0-img-8.jpeg](chunk-0-img-8.jpeg)

- Exploring the sky130A directory which is a part of the Openlane Working directory(As seen below)
- Also commands for navigation include, cd, Is, Is -al, Is -ltr, cd -, cat, etc.
![chunk-0-img-9.jpeg](chunk-0-img-9.jpeg)

We mainly use Is -ltr for listing the content in the directory and also cd ../ is really helpful for going back to a directory.

- Exploring the libs.ref directory which contains all the tech stuff in it, as seen below:
```
drwxr-xr-x 11 vsduser docker 4096 Jun 28 2021 libs.tech
drwxr-xr-x 14 vsduser docker 4096 Jun 28 2021 libs.ref
-rwxr-xr-x 1 vsduser docker 170 Jun 28 2021 SOURCES
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/pdks/sky130A$ cd 1
libs.ref
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.
ref$ ls -ltr
total 48
drwxr-xr-x 10 vsduser docker 4096 Jun 28 2021 sky130_osu_sc_t18
drwxr-xr-x 12 vsduser docker 4096 Jun 28 2021 sky130_fd_sc_ms
drwxr-xr-x 12 vsduser docker 4096 Jun 28 2021 sky130_fd_sc_ls
drwxr-xr-x 12 vsduser docker 4096 Jun 28 2021 sky130_fd_sc_hdll
```

- libs.tech is specific to the tool whereas libs.ref is specific to the technology.
- As seen below, this is the content of the libs.tech directory:
![chunk-0-img-10.jpeg](chunk-0-img-10.jpeg)
- Exploring the sky130_fd_sc_hd file which contains all the technological files like lef, techlef, etc.
![chunk-0-img-11.jpeg](chunk-0-img-11.jpeg)

- Exploring the lib file under sky130_fd_sc_hd directory
![chunk-0-img-12.jpeg](chunk-0-img-12.jpeg)
- As you can see above, I cd'ed into the file and Is -ltr'ed it to show me the content in chronological order.

Working on my own- exploring the techlef file (As seen below):

```
drwxr-xr-x 1 vsduser docker 12837196 Jun 28 2021 sky130_fd_sc_hd__ss_n40C_1v28.11b
drwxr-xr-x 1 vsduser docker 12844125 Jun 28 2021 sky130_fd_sc_hd__ss_100C_1v40.11b
rwxr-xr-x 1 vsduser docker 12845948 Jun 28 2021 sky130_fd_sc_hd__ss_100C_1v40.11b
drwxr-xr-x 1 vsduser docker 71255250 Jun 28 2021 sky130_fd_sc_hd__ff_n40C_1v95.11b
drwxr-xr-x 1 vsduser docker 71255751 Jun 28 2021 sky130_fd_sc_hd__ff_n40C_1v95_ccsnotse.11b
drwxr-xr-x 1 vsduser docker 12842851 Jun 28 2021 sky130_fd_sc_hd__ff_n40C_1v76.11b
drwxr-xr-x 1 vsduser docker 712842973 Jun 28 2021 sky130_fd_sc_hd__ff_n40C_1v65.11b
drwxr-xr-x 1 vsduser docker 12842102 Jun 28 2021 sky130_fd_sc_hd__ff_n40C_1v56.11b
drwxr-xr-x 1 vsduser docker 12841550 Jun 28 2021 sky130_fd_sc_hd__ff_100C_1v95.11b
rsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dlr/pdfs/sky130A/11bs.ref/sky130_fd_sc_hd/11b$ }
```


# Design preparation: 

- Going into the Openlane directory after clearing and going back usign cd command.

![chunk-0-img-13.jpeg](chunk-0-img-13.jpeg)

- We use docker to actually get in to openlane, as shown below:

```
vsduser@vsdsquadron: /Desktop/work/tools/openlane_working_dir/openlane\$ docker
Hash:4.25 ls -ltr
total 136
drwxr-xr-x 1510009974096 Jun 292021 scripts
drw-r--r-- 1100099720787 Jun 292021 run_designs.py
drw-r--r-- 110009977898 Jun 292021 report_generation_wrapper.py
drwxr-xr-x 310009974096 Jun 292021 regression_results
drwxr-xr-x 110009976519 Jun 292021 flow.tcl
drwxr-xr-x 510009974096 Jun 292021 docs
drwxr-xr-x 510009974096 Jun 292021 docker_build
drwxr-xr-x 4410009974096 Jun 292021 designs
drwxr-xr-x 210009974096 Jun 292021 configuration
drw-r--r-- 110009975514 Jun 292021 conf.py
drwxr-xr-x 11000997966 Jun 292021 clean_runs.tcl
drw-r--r-- 1100099725509 Jun 292021 README.md
drw-r--r-- 110009977273 Jun 292021 Makefile
drw-r--r-- 1100099711350 Jun 292021 LICENSE
drw-r--r-- 110009971285 Jun 292021 CONTRIBUTING.md
drw-r--r-- 11000997709 Jun 292021 AUTHORS.md
drw-r--r-- 110001000963 May 192023 default.cvcrc
Hash-4.25 SS
```


# Getting into openlane tcl: 

![chunk-0-img-14.jpeg](chunk-0-img-14.jpeg)

Openlane 0.9 implementation:
![chunk-0-img-15.jpeg](chunk-0-img-15.jpeg)

Anything that runs on openlane is extracted from the designs folder.

- Opening a new terminal window to explore the design file in the openlane dir, as show below:
![chunk-0-img-16.jpeg](chunk-0-img-16.jpeg)
- After this, I explored the picorv32a dir in the design dir, as shown below:
![chunk-0-img-17.jpeg](chunk-0-img-17.jpeg)

Checking out the content in the config.tcl file:
![chunk-0-img-18.jpeg](chunk-0-img-18.jpeg)
![chunk-0-img-19.jpeg](chunk-0-img-19.jpeg)

Content inside the sky130A_sky130_fd_sc_hd_config.tcl file by using the "less" command:
\# SCL Configs
set : :env(GLB_RT_ADJUSTMENT) 0.1
set : :env(SYNTH_MAX_FANOUT) 6
set : :env(CLOCK_PERIOD) "24.73"
set : :env(FP_CORE_UTIL) 35
set : :env(PL_TARGET_DENSITY) [ expr (\$::env(FP_CORE_UTIL)+5) / 100.0 ]
END

Preparing design in openlane(first step) as seen below:
![chunk-0-img-20.jpeg](chunk-0-img-20.jpeg)
-As we can see, A new file was created,named "runs" after we ran preparation in openlane:

```
<vsduser@vsdspuadron: /Desktop/work/tools/openlane_working_dir/openlane = < vsduser@vsdspuadron: /Desktop/work/tools/
vsduser@vsdspuadron: /Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a$ ls -ltc
Total 28
drwxr-xr-x 2 vsduser docker 4096 Jun 29 2021 src
drw-r--r-- 1 vsduser docker 209 Jun 29 2021 sky130A_sky130_fd_sc_ms_config.tcl
drw-r--r-- 1 vsduser docker 209 Jun 29 2021 sky130A_sky130_fd_sc_ls_config.tcl
drw-r--r-- 1 vsduser docker 209 Jun 29 2021 sky130A_sky130_fd_sc_hdll_config.tcl
drwxr-xr-x 1 vsduser docker 209 Jun 29 2021 sky130A_sky130_fd_sc_hd_config.tcl
drwxr-xr-x 1 vsduser docker 444 Jun 29 2021 config.tcl
drwxr-xr-x 3 vsduser vsduser 4096 Jul 17 01:22 runs
vsduser@vsdspuadron: /Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a$
```

# Review files after design prep and run synthesis 

- Folder structures required by OpenLANE, (It automatically shows current date as well), As seen below:
![chunk-0-img-21.jpeg](chunk-0-img-21.jpeg)

This is the content in the date file:

[^0]
[^0]:    -merged .lef folder, This was created when we ran OpenLANE Seen below:

![chunk-0-img-22.jpeg](chunk-0-img-22.jpeg)

This is the content inside the merged_unpadded.lef file in the synthesis dir
![chunk-0-img-23.jpeg](chunk-0-img-23.jpeg)

- Inside the logs dir:
![chunk-0-img-24.jpeg](chunk-0-img-24.jpeg)
- $\quad$ Parameter/Content inside the config.tcl file:
![chunk-0-img-25.jpeg](chunk-0-img-25.jpeg)
- Content/Data inside the cmds.log (command file), as shown below:

[^0]
[^0]:    1. 1st 16 16:11-15 177 2013 - Executing "gethost .myms.d8_ Flow/cn/tats/mct/wit_metal_Tapers_an -1 _Flame/roduser/desktop/work/tools/openlane_worting_dir/gs8u/obj138e/116c.1ef/obj138_fd_sc_bd/mot1ef/obj138_fd_sc_bd_116f -2 .myms.d8_ Flow/designs/picerv32a/runs/16-07_29-31/majmet_tapers_11st.txt"
    2. 1st 16 16:11-15 177 2013 - Executing "myms.d8_ Flow/cn/tats/merapost_an -1 _Flame/roduser/desktop/work/tools/openlane_worting_dir/gs8u/obj138e/116c.1ef/obj138_fd_sc_bd/mot1ef/obj138_fd_sc_bd_116f -2 .myms.d8_ Flow/designs/picerv32a/runs/16-07_29-31/majmet_tapers_11st.txt"
    3. 1st 16 16:11-15 177 2013 - Executing "myms.d8_ Flow/cn/tats/merapost_an -1 _Flame/roduser/desktop/work/tools/openlane_worting_dir/gs8u/obj138e/116c.1ef/obj138_fd_sc_bd/mot1ef/obj138_fd_sc_bd_116f -2 .myms.d8_ Flow/designs/picerv32a/runs/16-07_29-31/majmet_tapers_11st.txt"

# OpenLANE Project Git Link Description 

## Github link: https://github.com/efabless/openlane

![chunk-0-img-26.jpeg](chunk-0-img-26.jpeg)

- Synthesis : Success

| 11. Executing terting backend. <br> umping module 'jpicerv32a'. |  |  |  |  |  |  |  |  |  |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| arnings: 307 unique messages, 307 total <br> nd of script: cagfile hash: s4a4171f28, CPD: user 16.78s system 1.68s, MER: 96.33 MB peak <br> guys 8.8x3021 (git chat 84e9faf, gcc 8.3.1 -f915 -0s) <br> line opens: 108 12 db: 133 sec1, 138 32s apt_kep: 14 sec1, ... <br> 108011 (hopping module: true 8 or hopenLANt, lineDesigns/picerv32a/runs/16-87_19-32/results/synthesis/picerv32a.synthesis. <br> 108011: Running Static Timing Manual? <br> 108011: Current Data Tables? <br> pem116 2.3.8 08b48383a8 Copyright (c) 2019, Parallax Software, Inc. <br> license GPLsi: 100 GPL version 1 -http://gpu.org/licenses/gpl.html> |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |


# - OpenLANE Flow: 

![chunk-0-img-27.jpeg](chunk-0-img-27.jpeg)

Must follow this in order to run commands, not following this will result in break the subsequent commands, as seen below:

Then, you should be able to run the following commands:
0 . Any tcl command.

1. prep -design <design> -tag <tag> -config <config> -init_design_config -overwrite similar to the command line arguments, design is required and the rest is optional
2. run_synthesis
3. run_floorplan
4. run_placement
5. run_cts
6. run_rout.ing
7. run_magic
8. run_magic_spice_export
9. run_magic_drc
10. run_netgen
11. run_magic_antenna_check

The above commands can also be written in a file and passed to flow.tcl :

# Steps to characterize synthesis results 

sky130_fd_sc_hd__dfxtp_2 size: 1613<br>Total Number of cells : 14876

Ratio : 10.84\%

- Checking our runs folder after running synthesis
![chunk-0-img-28.jpeg](chunk-0-img-28.jpeg)

As we can see a new file, picorv32a.synthesis.v has been created in the results dir of the synthesis due to the synthesis

- Reports of the synthesis in chronological order, as shown below:

| mduser@vsdsquadroni=/Desktop/work/tools/openlane_working_dlr/openlane/designs/picorv32a/runs/16-07_19-52/reports/synthesis\$ ls -ltr <br> 1st 1736 |  |  |  |  |  |
| :--: | :--: | :--: | :--: | :--: | :--: |
| $2 w-r--r--1$ | vsduser vsduser | 1216 | Jul 17 | 12:14 | 1-yosys_pre.stat |
| $2 w-r--r--1$ | vsduser vsduser | 866 | Jul 17 | 12:14 | 1-yosys_dff.stat |
| $2 w-r--r--1$ | vsduser vsduser | 28479 | Jul 17 | 12:15 | 1-yosys_4.chk.rpt |
| $2 w-r--r--1$ | vsduser vsduser | 2674 | Jul 17 | 12:15 | 1-yosys_4.stat.rpt |
| $2 w-r--r--1$ | vsduser vsduser | 12 | Jul 17 | 12:15 | 2-opensta_tns.rpt |
| $2 w-r--r--1$ | vsduser vsduser | 11 | Jul 17 | 12:15 | 2-opensta_wns.rpt |
| $2 w-r--r--1$ | vsduser vsduser | 816771 | Jul 17 | 12:15 | 2-opensta.timing.rpt |
| $2 w-r--r--1$ | vsduser vsduser | 17763 | Jul 17 | 12:15 | 2-opensta.min_max.rpt |
| $2 w-r--r--1$ | vsduser vsduser | 816771 | Jul 17 | 12:15 | 2-opensta.rpt |
| $2 w-r--r--1$ | vsduser vsduser | 74793 | Jul 17 | 12:15 | 2-opensta.slew.rpt |
| mduser@vsdsquadroni=/Desktop/work/tools/openlane_working_dlr/openlane/designs/picorv32a/runs/16-07_19-52/reports/synthesis\$ |  |  |  |  |  |

- Contents of the 1-yosys_4.stat.rpt report

# 4. Existing statistics. 

## picorv32a

Number of wires: 14596
Number of wire bits: 14978
Number of public wires: 1565
Number of public wire bits: 1947
Number of memories: 0
Number of memory bits: 0
Number of processes: 0
Number of cells: 14876
sky138_fd_so_hd__a2111o_2 1
sky138_fd_so_hd__a211o_2 35
sky138_fd_so_hd__a211o_2 60
sky138_fd_so_hd__a21ho_2 149
sky138_fd_so_hd__a21ho1_2 0
sky138_fd_so_hd__a21o_2 57
sky138_fd_so_hd__a21o1_2 244
sky138_fd_so_hd__a221o_2 86
sky138_fd_so_hd__a22o_2 1013
sky138_fd_so_hd__a2bh2o_2 1740
sky138_fd_so_hd__a2bh2o1_2 81
sky138_fd_so_hd__a311o_2 2
sky138_fd_so_hd__a31o_2 49
sky138_fd_so_hd__a31o1_2 7
sky138_fd_so_hd__a32o_2 40
sky138_fd_so_hd__a41o_2 1
sky138_fd_so_hd__and2_2 157
sky138_fd_so_hd__and3_2 50
sky138_fd_so_hd__and4_2 345
sky138_fd_so_hd__and4b_2 1
sky138_fd_so_hd__bof_1 1656
sky138_fd_so_hd__bof_2 0
sky138_fd_so_hd__camb_1 42
sky138_fd_so_hd__dfw1p_2 1613
sky138_fd_so_hd__1no_2 1015
sky138_fd_so_hd__mos1_1 1224
sky138_fd_so_hd__mos2_2 2
sky138_fd_so_hd__mos4_1 221
sky138_fd_so_hd__nand2_2 70
sky138_fd_so_hd__nor2_2 524
sky138_fd_so_hd__nor2b_2 1
sky138_fd_so_hd__nor4_2 42



