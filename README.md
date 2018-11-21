# Smart Home Project
## 1. Motivation
I've always loved automations and to automate, that's why I enjoy software engineering and informatics in general, but I've have never imagined I could've actually automate lots of stuff I do at home.

After fiddling with [Amazon Alexa](https://developer.amazon.com/alexa) and realizing the power of the voice recognition-powered, rich commands it had, and the simple routines and automations it provided natively, I craved for more. I bought some generic Wi-Fi RGB light bulbs and Wi-Fi power switches and connected them to my Echo Dot, and voilá: I now could *control* my lights and power switches *with my voice*. Little did I know that I started a journey towards home automation and the **Smart Home** movement that would improve my life tenfold (and provide me with a hobby and tinkering entertainment).

### 1.1.  Encountered limitations
When adding lots of devices, with different types (sensors, lights, switches), into my smart home ecossystem, through Alexa's smart home provided services, I realized it was kind of limited. Even though it provided lots of automation capabilities, it lacked the flexibility I wanted. I realized that some devices just couldn't communicate with one another in the way I wanted them to. 
My brother-in-law recommended me to look at [Xiaomi's Smart Home](https://xiaomi-mi.com/mi-smart-home/) ecossystem, which, even though was amazing, cheap. and with lots of devices, they couldn't communicate with my other devices due to their lack of connection to Xiaomi's Hub. I didn't want to replace them, since I already invested money in them, so I looked for another solution. This is when I encountered [Home Assistant](https://www.home-assistant.io/).

### 1.2. Finding Home Assistant
[Home Assistant](https://www.home-assistant.io/) is an intermediary system that serves, pretty much, as a hub to all your configured devices. It runs on a local server (in my case a [Raspberry Pi 3 Model B+](http://a.co/ak2SQor) with 16GB of SD card memory) and allows for a very nifty database that saves my data locally, hence not requiring my data to be saved to the cloud. Home Assistant provides so many components that it's rare for you to own a device that is not compatible with its system. And even if you manage to get one of those, you can always code, with some trial and error, your own adapter to integrate it into your ecosystem. It isn't necessarily the most straightforward environment, you require lots of tinkering and configuration to get everything up and running, but it's very rewarding to do so. Even if you have no background in programming, or informatics in general, the community has loads of tutorials and it always eager to help you through your journey. 
When I found this I was thrilled: I could re-use all my devices and use the Xiaomi's smart home ecossystem while I was at it, and create a smart home system I was happy with.

----

## 2. Objectives
First, what I had to do was to define why I wanted to do a smart home system in the first place and this is my primary goal:

> **Doing less without losing control**

This goal is very broad, but it allowed my to subdivide, and organize, this into smaller goals:

| Section     | Systems                                                            | Devices |
|-------------|--------------------------------------------------------------------|---------|
| Better Comfort | automated lights and switches, media control, voice input   | bulbs, LEDs, power switches, motion sensors, smart televisions, chromecasts, echos |
| Better Security | surveillance, door & window state detection, vacant house mode | cameras, climate sensors, door sensors, presence sensors |
| Relevant Information | push notifications, TTS, family tracking, external information  (forecasts and traffic) | speakers, routers, device trackers, echos 


