
# Tractian Technical Challenge

## The problem

Develop a full wireless communication system. 

**Requirements:**
- Send a file of size 500kB;
- The devices should be 100m apart open-air;
- At least  one of the devices must be battery powered.

## The solution

### 1. Sketch it up!

The first challenge was to choose the communication protocoto match the requeriments. Wi-Fi, Zig-Bee and bluetooth was considered, but LoRa has been chosen as the communication protocol. The main reason for this choice was the energy requirement, LoRa is extremely energy-efficient and also capable of sending a 500kB through a 100m gap in a resonable amount of time.

Doing some research about LoRa on IoT forums I dicovered a new product from Microchip, the SAM R34 module. It is a System In a Package that contains the microprocessor and the LoRa module in a single chip. Besides this advantages, I preferred this solution because I've already make other projects with Microchips products., and i've had good impressions.


<!-- imagem do chip -->
![enter image description here](http://www.grupoautcomp.com.br/wp-content/uploads/2019/03/ic-tfbga-64pin-samr34-ps.png)

The next step was to dive deep into the SiP Datasheet and documentation, to understand the specificities of this microprocessor. After that I was capable of sketching a schematic. It is in the repository named  <!-- nome do arquivo -->

**Microcontroller**
![](https://i.ibb.co/yyt4CdD/image.png)

**RF circuit**
![](https://i.ibb.co/BsSNCs8/image.png)

**Oscillators**
![enter image description here](https://i.ibb.co/TT2GGXR/image.png)


**learnings:**

- When dealing with RF circuits it is import to add some decoupling capacitors to minimize interference, they act as low-pass filters and is import to place it right next to the chip terminals

### 2. It’s layout time
 
With the schematic on hand the PCB project started. As PCB design guidelines (and the SAMR34 datasheet) suggest boards with analog electronic, specially RF electronic, should be at least 4 layers, one being a ground plane, another being the power layer. Also, it's good to physically apart the components by their function, specially the RF components that can suffer from interference. 

![<!-- image of the sites -->](https://i.ibb.co/sbyjxYt/Screenshot-from-2022-12-19-00-41-28.png)

#### Controlled Impedance
To reduce reflectance of the signal on analog signal tracks it is import to tune the track impedance to match the internals of the RF module and antenna. In this implementation, 50$\Omega$. 

For reference, the PCB dimensions and tolerances are from JCLPCB JLC7628 Stackup.

|  Min. Trace width/Spacing  | Min. Via  |   Min. BGA |
|---:|---:|---:|
|3.5mil|0.2mm|0.25mm

**Prepeg/Core dieletric constant:**  4.6

**Stacking:**
| Layer         | Material Type | Thickness |
|---------------|---------------|-----------|
| Top Layer1    | Copper        | 0.035 mm  |
| Prepreg       | 7628*1        | 0.2104 mm |
| Inner Layer2  | Copper        | 0.0152 mm |
| Core          | Core          | 1.065 mm  |
| Inner Layer3  | Copper        | 0.0152 mm |
| Prepreg       | 7628*1        | 0.2104 mm |
| Bottom Layer4 | Copper        | 0.035 mm  |
| **Total**| --|1.5862 mm|

![enter image description here](https://i.ibb.co/chhNMYm/Screenshot-from-2022-12-19-03-08-22.png)

Therefore, all RF tracks were made with this tuned impedance in mind.

#### Final Result

**Layers except GND plane**

![enter image description here](https://i.ibb.co/2nRzX3c/image.png)


**3D view**
![enter image description here](https://i.ibb.co/Gk8Cv96/Screenshot-from-2022-12-19-03-32-25.png)

