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
* Created symbolic links for the sample project ‘inverter’
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

The starting page of Xschem!

![Two](https://user-images.githubusercontent.com/72557903/195265694-b6b96f63-6494-491e-98ea-76ee78e1f8d2.JPG)

* Okay now we make our CMOS INVERTER as shown-

![inverter_schematic](https://user-images.githubusercontent.com/72557903/195254933-f227c76f-2f7e-4162-941b-90f0c863ab15.JPG)

* After properly making the schematic, save it to a symbol and run a working test-bench with the various components. (Be careful not to add any sources on the symbol because this is not what we want. We will check the symbol's functioning on other file with the *inverter_tb* )<br />

![Sim](https://user-images.githubusercontent.com/72557903/195254937-f26452c7-2641-46fb-b7a2-2832e87364d8.JPG)

![SIM2](https://user-images.githubusercontent.com/72557903/195268038-8cbca9fc-bff2-481c-8bf5-d6375aad5c65.JPG)

![image](https://user-images.githubusercontent.com/72557903/195255111-0fec957b-a5d7-447c-a9f2-28329c67a1b2.png)

* **magic** -  Upon properly setting up, we can find the technology used as SKY130 and various layers of the technology! *magic -d XR* - Better 3D rendering for colors/symbols and *magic -d OGL* - Faster. <br />
* Documentation on magic! -http://opencircuitdesign.com/magic/tutorials/tut2.html
	
	1.Mouse 1- For placing <br />
	2.Mouse 3 - For resizing <br />
  	3.i-selecting a component <br />
	4.s-Select <br />
	5.%what - check component specs <br />
  	6.CTRL+p for parameter checks <br />
	*PS* -Moving is different than xschem, move to lower left hand corner and click M after using I
* CMOS Inverter in magic
![image](https://user-images.githubusercontent.com/72557903/195334075-2d321786-baab-4220-a5e5-57dc65ea06fa.png)


A sample NFET portray on magic!
![Three](https://user-images.githubusercontent.com/72557903/195254908-6ef9a459-e08d-4460-8725-2098b43bc980.JPG)

* Coming to our lovely inverter, when we import the contents to magic, we only get the various blocks scattered around. We have to use the various components and connect is as per our required diagram.( the figure shown is not properly connected, but this is a sample project lets see where this goes!)

![InverterLayout](https://user-images.githubusercontent.com/72557903/195268308-7fc231cf-ca46-4620-960b-160bf8864fe7.JPG)

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

	I learnt more about the lef command in this website.
		https://teamvlsi.com/2020/05/lef-lef-file-in-asic-design.html
	Lef files are associated with placement and routing, therefore we won’t find any transistors present in this particular view. (Abstract view)
    
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
(Incomplete)

## DAY 3
### DESIGN RULE CHECKING ( DEEP DIVE )
#### GLANCE INTO SILICON MAN PROCESS
1. Silicon manufacturing process is largely a planar process. The layers are added onto or implanted into other layers.

 ![image](https://user-images.githubusercontent.com/72557903/195252426-25c7cb76-11f5-40b0-b467-daad84dd01c7.png)
 
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

* The n-well beneath the p type transistor, as well as the source and drain of both n and p type transistors, can withstand greater voltages thanks to high voltage implants in transistors. In order to prevent gate punch through at higher voltages, high voltage transistors also require thicker gate oxide layers. The high voltage layer has a lot of restrictions because the transistor is directly affected by it.  Transistor gates must be bigger and longer, and N-wells need more space between themselves and low voltage wells.

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
