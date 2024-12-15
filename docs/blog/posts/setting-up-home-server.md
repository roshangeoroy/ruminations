---
date: 2024-12-16
authors: [roshan]
description: >
    A stop to endless weekend dilly dallies
categories:
  - Blog
---

# Finally Set up a home server

I got me hands on a slick Ti Processor EVM - the SK-AM62x EVM. I spend this weekend tinkering around with it and set up a home server (finally!).
<!-- more -->

## Ti AM62x EVM  
After many weeks of waiting, I finally got my hands on this EVM. It houses the AM62 processor, which features a quad-core 64-bit ARM Cortex-A53 MPU and a single-core ARM Cortex-M4F MCU. This is my first time working with a processor after spending nearly two years working exclusively with MCUs (though I’m not sure if the nRF5340 SoC counts as a processor).  
![am-62]

The Processor SDK provides pre-built images, and I chose the Debian Trixie image to run on it. I spent an entire night trying to boot the device from an SD card, only to realize the next day that the issue was caused by the software I used to flash the image—**BalenaEtcher**. The problem seemed to be with the latest version of the software. Reverting to an older version did the trick, and I was finally able to get it running!  

### Services  
The EVM has only 2 GB of RAM, so setting up Jellyfin wasn’t an option. However, I managed to set up Home Assistant, something I had been wanting to do for a long time. The setup process was pretty straightforward. I decided to run it as a Docker container instead of using the full Home Assistant OS. Additionally, I set up **Portainer** to manage the Docker containers running on my server.  
![portainer]
![homeassistant]

Since I had Home Assistant running, I decided to pair it with a smart light. So, I made one myself.  


### Smart Light Box (I’ll think of a cooler name later)  
If you’ve read my previous posts, you might know that I have many LED strips and rings lying around. I repurposed one of them to create a cute little glowing box. I used the standard WLED firmware to control the strips. It even has direct integration with Home Assistant, which made my life so much easier!  
![light-box]{: style="height:750px;width:750px"}

### Ending Notes  
Overall, it was a fun and productive weekend! For the past couple of months, I had been doing nothing but sleeping during the weekends. Also, I want to learn **Astro** so I can port this website to it. I love the concept of the command palette in VS Code and similar features in ARC, and I want to incorporate something like that into my website. Unfortunately, I couldn’t find any implementation for it in MkDocs, so I decided to switch to Astro. Let’s see—hopefully, I’ll sit down to learn it next weekend!  


[light-box]: setting-up-home-server/light_box.gif
[portainer]: setting-up-home-server/portainer.png
[homeassistant]: setting-up-home-server/home-assistant.png
[am-62]: setting-up-home-server/am_62.gif