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
