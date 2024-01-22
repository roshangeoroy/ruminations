# Dimmer Light
After many years of wanting to have a dimmer light in my room, I decided to make one myself. The amount of times I have started an IoT project and left it unfinished is a __lot__. Those were mainly because of the heavy information dump. 

But now that I have 4-5 months of experience developing IoT projects, I feel confident enough to start my own project!  


The project will be divided into two :

* Dimmer Switch
* Dimmer Light

Dimmer switch would be a rotary knob with a switch action as well. There would be an interactive addrresable led ring around the knob that light up depending on the level indicated by the switch. I know, why would I need that when I am controlling light intensity of possibly the room? To answer that - I would be making the switch into a general level control switch that can be used to not only control the light, but also other devices. 

I intend to make these devices [Matter](https://csa-iot.org/all-solutions/matter/) enabled. This project would be a case study on the Matter Protocol as well.


## Hardware Requirements
The switch and the light will be made using different tech stacks to prove Matter is compatible with different microcontroller based devices.

### For Dimmer Switch 
* Seeed Studio XIAO ESP32C3 
* WS2812B led ring
* Rotary Encoder

### For Dimmer Light 
* TBD

## Software Requirements
The following softwares/tools are used to build the project. 

* ESP-IDF 
* ESP-IDF Matter SDK
* VS Code
* Chip Controller for Linux


## Functional Requirements

### Dimmer Switch Functional Requirements

The dimmer switch will mainly contain 2 type of controls
* Mode control
* Level Control

#### Mode Control
The dimmer switch will contain a pressable knob which can act as a GPIO Switch. This switch can be configured to switch between different modes in the device.
The main modes are 
* Light Level control
* TBD

#### Level Control
The dimmer switch's knob will rotate in either direction. Rotating clock wise will increase a configurable level in the application, while anti-clockwise will decrease the level. 
