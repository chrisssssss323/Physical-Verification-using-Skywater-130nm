# Physical-Verification-using-Skywater-130nm

![image](https://user-images.githubusercontent.com/72557903/195252666-574a2ea4-bf38-45ad-93bf-58552108ef1d.png)

## VSD-IAT WS - Physical Verification using SKY130
## SKY130 workshop documentation

**Organized by**: Kunal Gosh, Co-founder, VSD Corp. Pvt. Ltd. <br />
**Instructor** : Tim Edwards, works for Efabless and a open tools developer. <br />
**Assisted by**- Sumanto Kar, Sr. Project Technical Assistant, IIT Bombay. <br />

The workshop focusses on getting students to learn about DRC/LVS using Skywater 130nm technology.
Although this is a mid-advance course; me, as a newbie,  could learn many things related to the physical verification process.
Any doubt or query was instantly resolved by the heads and well as my peers.
(Pictures used in the documentation are created by Tim Edwards and VSD.)

## DAY 1

SKY130 is a joint effort by Google and SkyWater Technology Foundry, the SkyWater Open Source PDK offers a fully open source Process Design Kit and supporting resources that may be used to produce designs that can be manufactured at SkyWater's facilities.

https://github.com/google/skywater-pdk

This repository is intended for the SKY130 process node as of May 2020. The availability of nodes with more cutting-edge technologies may increase in the future if the SKY130 process node release is successful. 

Although several designs that have been successfully fabricated commercially in sizeable quantities have been created using the SKY130 process node and the PDK from which this open source release was developed, the open source PDK is not currently intended to be utilised in production settings. It ought to work for creating test chips and performing basic design verification.

#### Different steps to add PDK to local machine- 

	Clone the repository git clone https://github.com/RTimothyEdwards/open_pdks
	Run cd open_pdks
	Run ./configure --enable-sky130-pdk
	Run make
	Run sudo make install

*PS* - We were provided with a cloud-based learning environment for this wrokshop, so the entire process will be carried out in this.

#### The tools used are:

* magic 
* xschem
* netgen
* ngspice

#### The libraries supported by open_pdks are:

* Digital standard cells (ex: sky130_fd_sc_hd) 
* Primitive devices/analog (ex: sky130_fd_pr)
* I/O cells (ex: sky130_fd_io)
* 3rd party libraries (ex: sky130_ml_xx_hd)


### LAB

* Checked the installations of various tools that'll be used in this workshop.

* Created a directory for *inverter.
* Created folders for mag,xschem,ngspice
* Created symbolic links for the sample project ???inverter???
![One](https://user-images.githubusercontent.com/72557903/195254892-02b566d2-f485-4486-ac52-a6c0e13f841b.JPG)

#### Ideas about various tools is given along with the workflow!

* **xschem** -Schematic Editor that may be used to import schematics and produce nelists from them or to develop new schematics. To construct schematics, use the symbol libraries in Xschem. Both **ngspice** for analog simulation and **gaw** for examining waveforms are supported. Schematic of various components can be found and it can be clicked upon to view everything!

	1.Shift-I to insert stuff  <br />
	2.Hover+M for moving  <br />
	3.Hover+W for wiring  <br />
	4.Mouse 1 + q for props  <br />
	5.Various options of zoon can be seen on the upper tab. EG- CTRL+Z for zoom out , SHIFT +Z for zoom in
	7.Net-list +  Simulate  <br />
	8.Go back, turn LVS option on on original and quit.  <br />

The starting page of Xschem(.sch)!

![Two](https://user-images.githubusercontent.com/72557903/195265694-b6b96f63-6494-491e-98ea-76ee78e1f8d2.JPG)

* Okay now we make our CMOS INVERTER as shown-

![inverter_schematic](https://user-images.githubusercontent.com/72557903/195254933-f227c76f-2f7e-4162-941b-90f0c863ab15.JPG)

* After properly making the schematic, save it to a symbol and run a working test-bench with the various components. (Be careful not to add any sources on the symbol because this is not what we want. We will check the symbol's functioning on other file with the *inverter_tb* )<br />

![Sim](https://user-images.githubusercontent.com/72557903/195254937-f26452c7-2641-46fb-b7a2-2832e87364d8.JPG)

![SIM2](https://user-images.githubusercontent.com/72557903/195268038-8cbca9fc-bff2-481c-8bf5-d6375aad5c65.JPG)

![image](https://user-images.githubusercontent.com/72557903/195255111-0fec957b-a5d7-447c-a9f2-28329c67a1b2.png)

 * .sch -> .spice
 * 
* **magic** -  Upon properly setting up, we can find the technology used as SKY130 and various layers of the technology! *magic -d XR* - Better 3D rendering for colors/symbols and *magic -d OGL* - Faster. <br />
* Documentation on magic! -http://opencircuitdesign.com/magic/tutorials/tut2.html
	
	1.Mouse 1- For placing <br />
	2.Mouse 3 - For resizing <br />
  	3.i-selecting a component <br />
	4.s-Select <br />
	5.%what - check component specs <br />
  	6.CTRL+p for parameter checks <br />
	*PS* -Moving is different than xschem, move to lower left hand corner and click M after using I
	
A sample NFET portray on magic!
![Three](https://user-images.githubusercontent.com/72557903/195254908-6ef9a459-e08d-4460-8725-2098b43bc980.JPG)

* Coming to our lovely inverter, when we import the contents to magic, we only get the various blocks scattered around. We have to use the various components and connect is as per our required diagram.( the figure shown is not properly connected, but this is a sample project lets see where this goes!)

![InverterLayout](https://user-images.githubusercontent.com/72557903/195268308-7fc231cf-ca46-4620-960b-160bf8864fe7.JPG)

* Perform extraction using- <br />

		extract do local
		extract all
		ext2spcie lvs
		ext2spice
		quit

* .mag -> .ext -> .spice

* **ngspice** - Used to study the various characteristics of the design made. Plot functions based on various criteria is readily available.
* **netgen** - LVS utility that checks the layout design with its schematic between netlists to verify geometry.

* After joining the layouts, extract and perform lvs on the command line. If properly done, the netlists will be matched!

![Four](https://user-images.githubusercontent.com/72557903/195254920-1f316ab5-2e74-436d-8295-ddbc055ac5ae.JPG)
![Five](https://user-images.githubusercontent.com/72557903/195254923-95b4a37f-7d40-41e3-bfac-87b50a0ec565.JPG)

* Due to some errors , my netlists were not matched! But we'll get them next time.


![image](https://user-images.githubusercontent.com/72557903/195380267-009651ea-b3f4-45cf-8ae3-5b4e410105df.png)
*END OF DAY1*

## DAY 2

* Standard start, created a directory for the *lab2*, a directory for the mag file and loaded sky130 tech files into it.

Today, I came to know about the various cif styles that can be used:

cif listall istyle This lists all the available styles
cif list istyle This lists the current style
cif istyle sky130(vendor) is set

* Read gds files into the magic tkcon terminal and loaded it.

		cif istyle sky130 (vendor)
		gds ..
		gds noduplicates true (to avoid rewriting the file)
	
  
* Using cell manager, we see the components in the scroll list.
* Placed an AND2_1 gate
* Analysing various aspects of ports
* port first
* port 1 name,class,use (spits out default (GDS is bad at taking in metadata. But some order must be there to these ports, to analyze them))
* When we look into various aspects of the ports, we see that the .spice file has the ordering completely different to that of the gds.
* This is because the magic doesn't use the exact metadata of the gds file. Alternatively, the metadata can be captured from lef and spice files or cdl netlists.
* We use the lef command to solve this problem!
* I learnt more about the lef command in this website https://teamvlsi.com/2020/05/lef-lef-file-in-asic-design.html
* Lef files are associated with placement and routing, therefore we won???t find any transistors present in this particular view. (Abstract view)
    
* Now, we get proper annotation for different ports but still the .spice is not matched with the port ordering.
* So, we run the readspice from within the console and match orderings! <br />
readspice /usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/spice/sky130_fd_sc_hd.spice
* * This is really useful but might sometimes lead to errors due to abstract views.

![LefAbstractview](https://user-images.githubusercontent.com/72557903/195348415-476e12f1-daa6-4136-8a64-1ea485fcd3fc.JPG)

![PortsLEF](https://user-images.githubusercontent.com/72557903/195255262-d5d91710-eea8-4163-9919-c5049ceca80c.JPG)

* **Extraction**

		*extract all* <br />
		*ext2spice lvs* <br />
		*ext2spice cthresh 0* <br />
		*ext2spice* <br />
	
* **Full DRC**
	
![fulldrc](https://user-images.githubusercontent.com/72557903/195255295-470dc09d-58dd-4243-be25-25823c2cbbc0.JPG)

* **LVS**

		mkdir netgen 
		cd netgen
		cp /usr/share/pdk/sky130A/libs.tech/netgen/sky130A_setup.tcl ./setup.tcl
		cd ../mag
		magic -d XR sky130_fd_sc_hd__and2_1
		ext2spice lvs
		ext2spice lvs
		ext2spice
		quit
		cd ../netgen
		netgen -batch lvs "../mag/sky130_fd_sc_hd__and2_1.spice sky130_fd_sc_hd__and2_1" "/usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/spice/sky130_fd_sc_hd.spice sky130_fd_sc_hd__and2_1"



* **Setup for XOR**

		cd ../mag
		magic -d XR
		load sky130_fd_sc_hd__and2_1
		save altered
		load altered
		erase li
		flatten -nolabels xor_test
		load sky130_fd_sc_hd__and2_1
		xor -nolabels xor_test
		load xor_test
		quit
		magic -d XR
		load test3
		flatten -nolabels xor_test
		xor -nolabels xor_test
		load xor_test

## DAY 3
### DESIGN RULE CHECKING ( DEEP DIVE )
#### GLANCE INTO SILICON MAN PROCESS
1. Silicon manufacturing process is largely a planar process. The layers are added onto or implanted into other layers. 
2. All active, passive components , wires etc. are all defined by geometry in these layers.
3. **Masks** - High resolution stencils with some portions opacified. These are placed on our various layers and the photoresist is broken down. Now the ion implantation or acid etching can be carried out through the space created!

![image](https://user-images.githubusercontent.com/72557903/195314480-f9dc902c-4a73-4691-9850-d1a1535a5dd1.png)

As machines get better and better, the ability of us to congest the geometry of devices get better and better (Moore's law consequence).
Various other factors that affect the process include materials used, etching time, angle of etching etc. Spot defects are found out (shorts and opens) and if properly done, the distribution of dead chips will be certain percentage of the entire chip count.

![image](https://user-images.githubusercontent.com/72557903/195319611-db1eaf59-b0e0-4eca-a92c-bf5618e27064.png)

As the spacing is reduced the probability of failure increases exponentially!

DRC may suggest a minimum spacing to get a good process yield, if we space it wider than that, the process yield gets better, but more space is consumed! 

The DRC documentation of Skywater PDK can be found from-

https://skywater-pdk--136.org.readthedocs.build/en/136/rules.html

#### Metal layer rules

##### Width rule

![image](https://user-images.githubusercontent.com/72557903/195321017-b5137774-b7db-4b3a-962d-5298f400ec2a.png)

![image](https://user-images.githubusercontent.com/72557903/195321235-9a71995d-88ac-4e1a-ab7f-2aebdca235da.png)

* Feature size -Minimum width of a transistor that can be used. For SKY130, as the name suggests, it's 130nm. (But there's some misnomers associated with it)

##### Spacing rule

![image](https://user-images.githubusercontent.com/72557903/195323595-10a8b3e1-7290-42d3-9a13-b30231af67ec.png)

* Notably ,Skywater 130 doesn't need to account for run length rule.

##### Wide-spacing rule

* If one piece of the structure is wider than a given width, other wires of any width must be spaced apart at a greater distance.
* Metals >3 microns trigger widespacing rule in SKY130.


##### Notch rule

* Similar, if not the same, to spacing rule. But notch rule is associated with a fork geometry.

##### Minimum and maximum area rules

* Gives the minimum and maximum areas for a metal layer.
* Prevents delamination issues in the metal surface.

##### Minimum hole area rule

* Holes smaller than a particular dimension may lead to oxide layer may not completely fill it.

##### Contact cut (Via) rule

![image](https://user-images.githubusercontent.com/72557903/195327741-98e5c5ef-4225-450d-97df-4d4ae5c880bc.png)

* A minimal amount of metal must be present around contact cuts.
* Magic presents arrays of contact cuts for the same layer to layer connect as a single huge contact cut (via). It comprises of poly, contact cuts as well as local interconnects squeezed into one diagonal cuts squares.

#### Local Interconnect Rules

* In most foundry procedures, polysilicon layers are directly followed by aluminium. Between the polysilicon and metal layers, SkyWater uses local connection layers as routing layers. The rules for this layer are based on the material's physical characteristics, particularly its resistance per square.

#### Front-end rules

* These rules are device specific and an analog or a digital engineer need not care about this as they use standard cells which are already available which doesn't violate any DRC rules.
* MOSFETS  have various rules of minumum gate width, length spacing rules. Magic gives different device types for different forms of the same device( eg- pfet, lvtpfet, scpfet, etc)

#### Wells and taps

* **Tap is a region of space inside a well an has the same doping type as the well but opposite type of the implanted source or drain of the transistor**.
* Taps are naturally connected to the wells and specifically there to provide bias voltages so that the p-n junnctions formed by the MOSFET is reverse biased at all times to prevent any uncontrolled currents flowing through the MOSFET.
* There are spacing rules associated with taps and the transistor regions.
* **Same-net spacing rule**- If two well regions are of different nets there must be more spacing between tham than if they were part of the same net.

#### Deep n-well isolation

* Generally Deep-N well is used to isolate NMOS from the substrate of other NMOS.
For example suppose all the NMOS in a amplifier is kept in PWELL (common substrate ) and that is connectet to GND and there is another NMOS whose substrate is connected to other potential not to gnd. In that case you need to isolate that NMOS from other NMOS, otherwise substrate will get short. So to avoid this Deep-N well is used.

So, for that you have to put that particular NMOS in a Deep-N well Layer and that MOS should surround with a N-well guardring.
Here DeepNwell is act as a bottom side and the NWELL guardring is act as a sidewall to seperate that particular NMOS from common P-type substrate.

* It has huge minimum space and minimum width requirements.

#### High Voltage rules

* The n-well beneath the p type transistor, as well as the source and drain of both n and p type transistors, can withstand greater voltages thanks to high voltage implants in transistors. In order to prevent gate punch through at higher voltages, high voltage transistors also require thicker gate oxide layers. The high voltage layer has a lot of restrictions because the transistor is directly affected by it. ??Transistor gates must be bigger and longer, and N-wells need more space between themselves and low voltage wells.

#### Device rules

##### Resistors

* Resistors can be made out of diffusion layers, polysilicon layers or p-well regions deep inside n-wells.
* Polysilicon layers are the most used, and it can have varying resistive properties per square as needed by the designer. 
* It has some specific rules associated with it.
* It's easier sometimes to make the resistors by hand.

##### Capacitors

* *Types*- Varactor, MOSCAP, MiM and Vertical Parallel plate (VPP) or MoM
* MiM has a very high capacitance er unit area than VPPs.
* Aspect ratio regulations, bottom and top layer regulations, and antenna regulations are all applicable to MiMs.

##### Diodes

* Diodes can be formed by a well and a diffusion layer. So by definition, we can have lot of unwanted diode activities inside a transistor due to several parasitic diode forming between the different layers

##### Fixed layouts

Eg- Several devices like a PNP bipolar transistor is already present as a block in magic, so need not care about making them DRC satisfied, we just have to take care of the rules associated with spacing of this device between other devices!

#### Miscellaneous rules

* Present in the documentation under *X* category.
* These are not layer specific rules.

##### Off-grid errors

* magic has a really good system internally to prevent any off-grid errors.
* Only way to create an off-grid error in magic is by superposing non-manhattan layers

##### Angle limitations
* diff,tap,poly,contacts - 90 ( Must be rectangular )
* 45 degrees to all other layers

##### Seal-ring rules

#### Rules associated with problems that may arise

##### Latch-Up rules

![image](https://user-images.githubusercontent.com/72557903/195354677-5c6ff147-8ff5-44a0-8118-bdbf269b3e22.png)

* Parasitic PNP AND NPN creates a condition called latchup. When these lousy transitors get their EB jn forward biased, the transitor is basically short-circuited to the ground and the chip will be stuck-at-state until power supply is turned OFF. 
* This may be due to the fact that the tap bias voltage may be different to the voltage local to the PN junctions
* Therefore, there is a basic tap to diffusion distance.

##### Antenna rules

* A long metal line not attached to anything will accumulate charge and if this charge is not sinked it, it will develop into a very high voltage.
* This will affect a transitor closest to it very badly.
* One way to fix antenna violation is to provide a path to the ground through parasitic PN junction of diffusion.
* Make sure all digital block elements have diode placements.

##### Stress rules.

 * Slots are provided to ensure the mechanical stress at any point of the metal layer width doesn't exceed a certain limit. Slotting is provided in the direction of current flow.
* Critical corners when provided with proper pad frames can easily overcome stress rules at that point and designer may not worry about it.

##### Density rules

* To reduce *bumpiness* of the surface after oxide growth and polishing, we place metal layers and in between them add some 'fill metals', so the surface after polishing is evenly smooth.
* This is done because, any layers grown on top of this is critically affected by the layer beneath, so density rules make sense.
* Automatic fill generation tools take care of it for the most part.
* But for analog engineers it is a nightmare as the extra capacitances will give them a migraine.

##### Recommended rules (RR)
* eg- Using redundant vias

*in addition to DRC, ERC is also another criteria that must be checked. A chip may be ERC correct but may have DRC problems. (eg- Electrmigration and Over-voltage)*

###  LAB

* Cloned TimEdward's repo into our terminal and accessed magic from the directory.

![image](https://user-images.githubusercontent.com/72557903/195382484-8b6a2ada-4aa5-450b-a7dc-c8f128ce261a.png)

* **Exercise**

* We learn about the various errors that Tim has taught us during the lectures. ( The errors are marked as white dotted lines )

![image](https://user-images.githubusercontent.com/72557903/195383230-bda3ef4d-bce7-4658-bdfa-40e0b6958dbe.png)

* Placing the white box over the required area and performing a 'DRC Report' will tell you the exact reason for the error to be reported and the associated rule in brackets.
* While doing this, make sure you cover the white dots in the select box or else errors won't be reported.
* The white dots tell you the amount of length that must be added or removed to satify the DRC.
	1.?- DRC REPORT <br />
	2.b- dimensions <br />
	3.4- Shift left <br />
	4.6- Shift right <br />
	5.8 - Shift up <br />
	6.2 - Shift down <br />
	7.Shift + [2,4,6,8] - Stretch down,sides,up <br />
	8.A- select a layer within box <br />

* We can also use commands like move (moving) and stret (stretching) and e,w,n,s for directions.

![image](https://user-images.githubusercontent.com/72557903/195405223-d7d34d6d-b2dd-47ea-be83-87f9898d8a2a.png)

* **Exercise**

![image](https://user-images.githubusercontent.com/72557903/195414073-0e20ec2b-65e7-4199-95c8-3746211a97fd.png)

* Use of *cif see* command -
![image](https://user-images.githubusercontent.com/72557903/195408117-c2638548-88db-4128-ad86-40e829a2c7d3.png)
* Feedback why and clear can show you the area where contact cuts can be placed. If the space is too small its shows a feedback error.
* box command with options c(all sides),e,w,n,s can help in reshaping our selected box.

![image](https://user-images.githubusercontent.com/72557903/195413558-246ea3a8-6f83-4854-b244-6fc8bda28bfb.png)

* **Exercise**

<img src="https://user-images.githubusercontent.com/72557903/195414855-c6fb039c-2bb0-4f3b-a5ca-38df5860b2d0.png" width="500">

* Minimum area error occurs if there isn't sufficient area of a metal between interconnects.
* drc(fast) doesn't look into hole errors, so switch to drc(complete) and run *drc check*
* Select the require hole size fixing the error and erase space within hole!

<img src="https://user-images.githubusercontent.com/72557903/195417428-baba986c-6679-4486-aeee-b2d32f46ccec.png" width="500">

* **Exercise**

* ![image](https://user-images.githubusercontent.com/72557903/195603194-bff17f7a-418a-4966-98ae-e8c4395fb11e.png)

* n-wells require an n-tap by default. p-subs need not, butin case they do, they'll need a contact as a must.

![image](https://user-images.githubusercontent.com/72557903/195611739-82036f36-be10-4bc6-8ede-f2ec8d034d9f.png)

* **Exercise**

![image](https://user-images.githubusercontent.com/72557903/195533262-a40f6561-9977-42a7-b10c-4f157fc7dc30.png)

* **Exercise**
(Angle error and overloap rule)

Part 1

![image](https://user-images.githubusercontent.com/72557903/195854154-2fcdb8e1-0736-4ee2-a389-cd967df9d9e0.png)
![image](https://user-images.githubusercontent.com/72557903/195854750-8c0974f8-ebc3-47fa-9044-c2c5dd9f3f38.png)

Part 2

![image](https://user-images.githubusercontent.com/72557903/195855595-2c231049-2245-4e35-9a3c-e3c3f9a7b16a.png)
![image](https://user-images.githubusercontent.com/72557903/195861440-6b0d9f50-87c6-4c04-b7bc-b9d6a3f6b8a1.png)
* Erase the poly areas and remove angled edges of layers that magic doesn't support and comes out as DRC errors

* **Exercise**

* Final view after solving individual angled errors and well as errors due to overlap of non-manhattan layers.

![image](https://user-images.githubusercontent.com/72557903/195865983-7c122760-a483-489c-94eb-f5be7056be12.png)

* **Exercise**

* Seal ring is a layer that goes around the perimeter of the chip along the padframe and protects the chip from sawing and dicing.
* A seal ring generator is present that produces the correct seal ring shape by procedural script.
* We see that attempting to paint over the seal ring causes DRC issues.
* The proper tech file for the seal ring is not written as it is so abstract.

* **Exercise**

![image](https://user-images.githubusercontent.com/72557903/195869467-f531cf40-056c-4f0b-9d61-2a81bb26375e.png)

* On questioning these errors, we see that the n-well not only miss taps but theses taps must also be present at adequate distances from diffusion regions to prevent latchup conditions!
* We adjust the taps manually without using 'Place and Route' to clarify latchup errors.

### DAY 5

#### LVS (Layout vs Schematic)

##### Fundamentals of LVS

* The designer does both LVS and DRC before tapeout.
* The netlists produced by each of the processes is compared with each other and matched. After tapeout, its send to the foundry, where it does DRC again before final processes.
* LVS is done by comaring the schematic netlist and the layout netlist
* *netgen* is the Open Source tool for doing LVS and can understand ssimulatable formats like VerilogRTL and SPICE.

##### Schematics

* Schematics are made in Xschem with the components.
* The entire circuitry is converted into one big symbol with I/0 ports.
* The symbol is ran to check it's required working with a testbench and the waveforms are checked.


##### LVS Matching

* Purely comparsion based matching techniques.
* The main way of check is by checking connections of the cells that needs to be compared.
* eq- We got a cell with 100 connections to VDD and another with 99 connections to power rail. What may happen is that the circuit is not matched and each every connection in the cell will flag the same error.

* In magic, netlist can be generated by using -
		
		extarct do local
		extract all//1
		ext2spice lvs //2
		ext2spice
		
* To get the full parasitic extraction, we have to use some more commands in between-
		
		ext2sim labels on //after 1
		ext2sim
		extresist tolerance 10
		extresist all
		ext2spice cthresh 0.01 //after 2
		ext2spice extresist on
		
##### Netgen core matching algorithm

* End user need not know anythng about netgen for its single-use.

		netgen -batch lvs "file1_ckt1" \ "file2_ckt2" setup_file output_file

* netcmp - starting point of the tool . Flattens the circuit and considered no hierarchy.

* To study netgen, let's consider two circuits with n devices [1,2,3....] and n nets [1,2,3,4...] each.
* It makes a devices list and a nets list matching devices and nets
* eg- Devices list- ckt1-d1, ckt2-d1,ck1-d2, ck2-d2, etc
* Now each of these combos gets assigned a number.
* Each pin of each device gets assigned a number.
* After seeing the layout, each of the ckt-net combo is the netlist gets assigned a number depending on the device-pin/device-pin connections.
* Groups of nets gives a number to the elemtents in the device list and transforms it into partitions.
* These partitions iterate through the same process aain and again until there comes a unique 1:1 partition between netlist components.

##### Netgen pre-match analysis

* This is a hierarchical check. The hierarchies for each of the circuits is checked for a 1:1 match.
* This seems easy but usually layouts have additional hierachies to it that may not be reflected directly in the schematic. For example, a multifingered pfet (parameterized device)


##### Pin-checking and property checking

* Pin names are meaningless in a match algo. 
* But it does care about the number of pins. But it also should not care about pins that got no connections within the circuit. (proxy pins)
* Properties, especially parametric properties, must be matched!
* If there are multpile paralle devices of the same kind, these can be grouped into one for matching purposes.
* The properties that has to be lumped follows various strategies.
* eg - A W=20, M=1 PFET will be matched with W=1 PFETs with 20 of them M=20 connected in parallel.


### LAB

* Focusses on doing LVS with *netgen*
* We use Tim's sample repo to do various excercises in this section.

#### Simple LVS experiment

![image](https://user-images.githubusercontent.com/72557903/195617064-b736a008-0fb5-4f8d-9bac-f0a9d3072a59.png)
![image](https://user-images.githubusercontent.com/72557903/195632010-3d185434-e118-4dc2-a7ea-343ba8c835ec.png)

* Netgen doesn't care about pin names at the sub level; but it does at the top level because it cannot make any assumptions there.
* So, subcircuits having different pin names wont be raised as an error in netgen.


![image](https://user-images.githubusercontent.com/72557903/195639741-12a94349-d08f-4d31-9994-20858c2a34c4.png)

* See, even changing the subcircuit pin names, doesnt raise an error in netgen.

* If we totally swap the pins, we get a netlist match, but a top level pin matching error.

#### LVS with subcircuits and blackboxes

* To overcome writing lengthy command every time, we can actually create a bash script for the same.
* We tee content to a json file to to make it more parsable.
* run_lvs.sh

		#!/bin/sh
		netgen -batch lvs "netA.spice" "netB.spice test" /usr/share/pdk/sky130A/libs.tech/netgen/sky130A_setup.tcl exercise_2_comp.out -json | tee lvs.log
		echo ""
		../count_lvs.py exercise_2_comp.json | tee -a lvs.log
	
* *chmod a+x run_lvs.sh* to make this executable and tada!

* If we change the pins in blockboxes we encounter erros in the form of mismatches.

![image](https://user-images.githubusercontent.com/72557903/195762461-c72b9e09-98e8-4a0d-b0b2-df3db7cc2b7e.png)
* *Change of a subcircuit pin to a random pin name creaes an error and when we see the comp.out file we see that proxy pins are created.*

![image](https://user-images.githubusercontent.com/72557903/195764270-f7c4a062-99da-4ff5-a51e-a5863033f5ea.png)

* Now let's mess with the cell names. If we change the netA.spice cell1 -> cell4 let's see what comes of it.
![image](https://user-images.githubusercontent.com/72557903/195764798-edff52fe-f62d-4e16-a97c-8d8df2ee8173.png)

* Problem with black box cells is that we wouldn't know when a cell is treated as a blackbox.
* So we use the -blackbox option in our run_lvs.sh file to fix this.

![image](https://user-images.githubusercontent.com/72557903/195764871-a344f47a-32bb-4481-b59e-e8f3dd4361cb.png)
* *We see the indication of no matching elements for cell1 and cell4 in these files.*

#### Final example

* For our last example, let's take two files netA.spice and netB.spice with netA.spice defined as follows-
![image](https://user-images.githubusercontent.com/72557903/195766696-b024810a-c00a-4036-9330-5551a945bf97.png)
R -> Resistor, C -> Capacitor, D-> Diode

* If I now swap A and C in cell subcircuit cell1, I get the same error of mismatches.
![image](https://user-images.githubusercontent.com/72557903/195767617-4502caee-a7f7-4632-b6ac-ca24cdd2ef73.png)

* So what can we do to make the netgen not hink like this (Because swapping resistor pins won't change anything)
* To do so, modify the sky130A.setup.tcl file with the following change to the eof.

		permute "-circuit1 cell1" A C
		permute "-circuit2 cell1" A C
		
* Now netgen knows that the cell1 is both the cicuits are permutable.

![image](https://user-images.githubusercontent.com/72557903/195769887-01ad755f-378e-47a5-b90d-44d5a41e39b7.png)

* Point to be noted- If netgen notices that the subcircuit pins are mismatched, it'll not flag an error if it sees that the pins in both the circuits are used the same topologically( but mismatches will be shown)

#### Small analog block

* Full doc -https://github.com/efabless/caravel_user_project_analog
* **Power-On Reset**- Every time power is applied to a certain electrical device, a power-on-reset circuit generates resetting signals. By doing so, you can identify a known state in which the device always turns on or activates.

![image](https://user-images.githubusercontent.com/72557903/195773305-982042f6-b74c-452e-950d-901faeba1388.png)
* Turn the 'top-level netlist is a .subcircuit' option ON.
* Generate a netlist from the xschem and exit out.
------------------------------------------------------------------
![image](https://user-images.githubusercontent.com/72557903/195777590-8390de44-7cfd-4533-8a2b-bbb14324e0e1.png)
* In the mean-time lets see some things about resistors from the setup.tcl file*
* We see that the pins are interchangeable and see how series and parallel combinations are defined.
-----------------------------------------------------------------
* We dash out to the magic directory, open our .mag file and perform the extraction.
![image](https://user-images.githubusercontent.com/72557903/195780577-312aeac0-c6df-49d4-a9a9-3be5cb407861.png)

* We go to the netgen directory and see the contents of the *run_lvs_warpper.sh*
![image](https://user-images.githubusercontent.com/72557903/195781325-8f118524-7470-49cb-aa90-370fb520c695.png)

* Perform LVS
![image](https://user-images.githubusercontent.com/72557903/195782129-ae376e06-2c56-47e9-8f09-9946cc4b6ec9.png)

* A clear problem is being evident, the layout labels all the cells properly, but the .spice from the schematic doesn't. So, a lot of proxy pins are created on both subs.
![image](https://user-images.githubusercontent.com/72557903/195782630-8544233d-589a-4f8d-81a9-a7a4684a9521.png)

* So the need for a proper subcircuit definition becomes the need of the hour.
![image](https://user-images.githubusercontent.com/72557903/195783729-1ce71675-2fd5-4b21-9b88-b41f834d89b0.png)

* We do LVS with the xschem tb file as circuit2
![image](https://user-images.githubusercontent.com/72557903/195784791-00bb3c51-9288-4c1f-bac4-7d08785c9ba6.png)

* The layout has more hierarchical structure than the schematic.

#### Layout vs Verilog for standard cells

* Load digital PLL file into mag and extract using the usual commands.

![image](https://user-images.githubusercontent.com/72557903/195825522-801515df-970b-4b76-ac75-76d7efdb3c9c.png)

* Start of the verilog module
![image](https://user-images.githubusercontent.com/72557903/195826281-498d1bb4-8aa6-4214-a526-d465a5019cea.png)

* LVS
![image](https://user-images.githubusercontent.com/72557903/195827200-f7ba389c-d09f-4565-9ea4-597e6c6bfd17.png)

* The problem-causing FILLER_0_11!
![image](https://user-images.githubusercontent.com/72557903/195829565-f3bb317d-52fb-4fc0-ba53-c4cc874cb46b.png)

* After going through the setup.tcl file and understanding that the environment variable needs to be added to the run_lvs.sh by
		
		export MAGIC_EXT_USE_GDS=1
		
![image](https://user-images.githubusercontent.com/72557903/195831461-d0ca2ce1-57ec-41eb-a958-98a6bc4749b6.png)

#### LVS FOR MACROS

* Load mgmt_protect file onto magic and do the required extraction.
* After performing LVS with the verilog file and the extracted mag file, we get the following message.

![image](https://user-images.githubusercontent.com/72557903/195833774-33bdac83-4a40-49bb-8685-2735297f66c3.png)

* Why is this error coming about? This is because of some behavioural nature in the verilog code.
* When we look into the *mgmt_protect.v*, wee see that at line 244, a seemingly harmless '~' does the trouble.

![image](https://user-images.githubusercontent.com/72557903/195834898-3543e6cc-ead0-4d05-8db3-48568f40112e.png)

* After using the actual gate-level .v file from the /verilog/ dir, let's run the LVS again

![image](https://user-images.githubusercontent.com/72557903/195835745-d3e9b854-8e95-4ac0-a6c6-547f8555b76d.png)

* There are still some errors to be handled. In terms of Magic, they have been combined with other gnd pins. Layout tools frequently act in this way when representing substrates for substrate connection. In order to address this, Magic has a layer called isosub that isolates substrate layers, although at the moment, Magic cannot isolate more than one substrate layer simultaneously. This function is still being developed.

* When we finally do the required connections to ground and run the LVS script again we see that the mismatch errors have been completely removed.

#### LVS DIGITAL PLL

* Extraction of digital PLL

![image](https://user-images.githubusercontent.com/72557903/195841838-51e69610-757a-4fe9-a2fa-bbd6c8f52458.png)

* Running LVS with netgen

![image](https://user-images.githubusercontent.com/72557903/195841965-69d1918d-e27e-46c1-8da0-da51dabdb561.png)

* On examining the the comp.out file we see that the subcircuits produce no error mismatches as expected, but the top level shows some device mismatches.

![image](https://user-images.githubusercontent.com/72557903/195842461-4a2a60f4-3a17-48b4-a4c5-c492f5521615.png)

* After doing the same solution used in the earlier exercise, we can use the change in the script and run LVS again.

		export MAGIC_EXT_USE_GDS=1

![image](https://user-images.githubusercontent.com/72557903/195843986-c744dd66-4baa-4e32-a499-ca719f4bbff9.png)

* On *greg*-ing our way into the .v and .mag files to check for *diode*, we see that the content is not present in th .v file but only in the .mag file.

![image](https://user-images.githubusercontent.com/72557903/195845080-daa860e3-5a56-47f8-9a70-bac236453977.png)

* Adding diode to our verilog file with the same instances and connections as our layout is done, and the missing diode instance problem in the verilog portion of the code is solved.

* From the layout, we curate the errors due to power supply problems.
## REFERENCES

* All pictures (other than the necessary screenshots from my own machine) for explanations is taken from Tim Edward's presentations SKYWATER PDK.
* https://web.stanford.edu/class/ee133/handouts/general/spice_ref.pdf ( For knowledge on how to read SPICE files)
* https://www.skywatertechnology.com/
* http://opencircuitdesign.com/

