# Physical-Verification-using-Skywater-130nm
VSD-IAT WS - Physical Verification using SKY130
SKY130 workshop documentation
![image](https://user-images.githubusercontent.com/72557903/195252666-574a2ea4-bf38-45ad-93bf-58552108ef1d.png)

Organized by: Kunal Gosh, Co-founder, VSD Corp. Pvt. Ltd.
Assisted by - Sumanto Kar, Sr. Project Technical Assistant, IIT Bombay
Instructor: Tim Edwards, works for Efabless and a open tools developer.

## DAY 1

Introduction to Skywater PDK
Opensource EDA Tools
Understanding Skywater PDK - Layers
Understanding Skywater PDK - Devices
Understanding Skywater PDK Libraries
Opensource Tools And Flows

#### Different steps to add PDK to local machine- 

Clone the repository git clone https://github.com/RTimothyEdwards/open_pdks
Run cd open_pdks
Run ./configure --enable-sky130-pdk
Run make
Run sudo make install

PS- We were provided with a cloud-based learning environment for this wrokshop, so the entire process will be carried out in this.

#### The libraries supported by open_pdks are:

Digital standard cells (ex: sky130_fd_sc_hd) 
Primitive devices/analog (ex: sky130_fd_pr)
I/O cells (ex: sky130_fd_io)
3rd party libraries (ex: sky130_ml_xx_hd)


## LAB 1

Created symbolic links between various files for the project ‘inverter’

xschem - Schematic of various components can be found and it can be clicked upon to view everything!

1.Shift-I to insert stuff

2.Hover+M for moving

3.Hover+W for wiring

4.Mouse 1 + q for props

5.After properly making the schematic, save it to a symbol and run a working test-bench with the various components.

6.Net-list +  Simulate

7.Go back, turn LVS option on on original and quit.

Magic -  Upon properly setting up, we can find the technology used as SKY130 and various layers of the technology!

1.magic -d XR - Better 3D rendering for symbols.

2.magic -d OGL - Faster

	Mouse 1- For placing
	Mouse 3 - For resizing
  
I -selecting a component

S-Select 
	%what - check component specs
  
	(Moving is different than xschem, move to lower left hand corner and click M after using I)
(Ctrl+p for param)

After joining the layouts, extract and perform lvs on the command line. If properly done, the netlists will be matched!
![One](https://user-images.githubusercontent.com/72557903/195254892-02b566d2-f485-4486-ac52-a6c0e13f841b.JPG)

![Two](https://user-images.githubusercontent.com/72557903/195254852-dfbe9859-2151-4ddf-94ba-7a501b81b7bc.JPG)
![Three](https://user-images.githubusercontent.com/72557903/195254908-6ef9a459-e08d-4460-8725-2098b43bc980.JPG)
![Four](https://user-images.githubusercontent.com/72557903/195254920-1f316ab5-2e74-436d-8295-ddbc055ac5ae.JPG)

![Five](https://user-images.githubusercontent.com/72557903/195254923-95b4a37f-7d40-41e3-bfac-87b50a0ec565.JPG)
![inverter_schematic](https://user-images.githubusercontent.com/72557903/195254933-f227c76f-2f7e-4162-941b-90f0c863ab15.JPG)

![Sim](https://user-images.githubusercontent.com/72557903/195254937-f26452c7-2641-46fb-b7a2-2832e87364d8.JPG)

## DAY 2
## LAB 2
Standard start, created a directory for the lab, a directory for the mag file and loaded contents into it.

Read gds files into the magic tkcon terminal and loaded it.

	cif istyle sky130 (vendor)
	gds ..
	gds noduplicates true (to avoid rewriting the file)
  
Using cell manager, we see the components in the scroll list.

Placed an AND2_1 gate

Analysing various aspects of ports

port first

port 1 name,class,use (spits out default (GDS is bad at taking in metadata. But some order must be there to these ports, to analyze them))

When we look into various aspects of the ports, we see that the .spice file has the ordering completely different to that of the gds.

We use the lef command to solve this problem!
		https://teamvlsi.com/2020/05/lef-lef-file-in-asic-design.html
		Lef files are associated with placement and routing, therefore we won’t find any transistors present in this particular view. (Abstract view)
    
Now, we get proper annotation for different ports but still the .spice is not matched with the port ordering.

So, we run the readspice from within the console and match orderings!

This is really useful but might sometimes lead to errors due to abstract views.

## DAY 3
### DESIGN RULE CHECKING ( DEEP DIVE )

1. Silicon manufacturing process is largely a planar process. The layers are added onto or implanted into other layers.
2. ![image](https://user-images.githubusercontent.com/72557903/195252426-25c7cb76-11f5-40b0-b467-daad84dd01c7.png)

