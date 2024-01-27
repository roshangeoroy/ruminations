---
date: 2024-01-28
authors: [roshan]
description: >
    It's a work in progress.
categories:
  - Blog
  - Project Updates
  - Matter
---

# Work in Progress

The project has reached its first milestone. As the saying goes, the first step is often the most challenging, and this was certainly the case here.

<!-- more -->

## Setting up the Development Environment

The full setup of the SDK - ESP IDF and familiarizing with it really took me a few days. But now that I'm feeling comfortable with it, I can say this is far better than using the Arduino IDE for programming ESP chips. We literally have control over everything.

I started off with prototyping code for the rotary encoder and the addressable LEDs. I got both working individually and somewhat together. The only problem is there is a huge latency between increasing the counter value and setting LED lights.

My favorite part was developing the state machine for the Rotary Encoder. This state machine eliminates much of the noise generated between detents. The state machine is based on [Mo-Thunderz's](https://github.com/mo-thunderz/RotaryEncoder) Rotary Encoder driver for Arduino, which was actually based on [Oleg Mazurov's](https://github.com/mo-thunderz/RotaryEncoder) driver for Arduino. I took the gist of both and made my own.

## LEDs are so fancy!

LEDs are fascinating but confusing. I straight out copied the RMT-LED example provided by ESP-IDF, but soon I will learn what exactly this RMT peripheral does. Maybe by next week, I will have a low latency switch control going on, to which I can integrate the matter (or to the matter example, I would integrate this, heh).

![lights]

## Blog Experience

Regarding the blog experience, it's been fun. I look forward to writing here. I might ask some of my friends to contribute here at times. Also might add an RSS feature so anyone reading this can stay updated, heh.


[lights]: work-in-progress/lights.png
