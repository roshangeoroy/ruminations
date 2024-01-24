---
date: 2024-01-25
authors: [roshan]
description: >
    Components has arrived for the project I am working on
categories:
  - Blog
  - Project Updates
  - Matter
---
# Components has arrived!
Finally I have everything to start working with. The components arrived earlier this week and this is how my desk looks now!

![workspace]
<!-- more -->
Started today with testing the LED strip. I used RMT examples provided by ESP-IDF itself to test out the leds. Did a bit of soldering- rough mostly because this is just the prototyping stage. I wasn't able to verify the proper working of the Rotary Encoder. I tried flashing an Arduino code I found online to the esp32 xiao board, but the rotary encoder wasn't giving proper output for it. I need to take it over to an oscilloscope to verify if the encoder is generating proper quadrature waveforms. 

Will integrate the firmware for led and encoder together in the coming week. I also have to decide if I should spend some time picking up CPP. Because, almost all Matter examples provided in the ESP-Matter SDK are written in CPP. Since I have a bit of background in python and Java, picking up CPP wouldn't be that hard. I had found this YT playlist, but I don't know if it's worth the time






[workspace]: components/workspace.png