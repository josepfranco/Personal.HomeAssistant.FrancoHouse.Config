# Smart Home Project
## 1. Motivation
I've always loved automations and to automate, that's why I enjoy software engineering and informatics in general, but I've have never imagined I could've actually automate lots of stuff I do at home.

After fiddling with [Amazon Alexa](https://developer.amazon.com/alexa) and realizing the power of the voice recognition-powered, rich commands it had, and the simple routines and automations it provided natively, I craved for more. I bought some generic Wi-Fi RGB light bulbs and Wi-Fi power switches and connected them to my Echo Dot, and voilá: I now could *control* my lights and power switches *with my voice*. Little did I know that I started a journey towards home automation and the **Smart Home** movement that would improve my life tenfold (and provide me with a hobby and tinkering entertainment).

### 1.1.  Encountered limitations
When adding lots of devices, with different types (sensors, lights, switches), into my smart home ecossystem, through Alexa's smart home provided services, I realized it was kind of limited. Even though it provided lots of automation capabilities, it lacked the flexibility I wanted. I realized that some devices just couldn't communicate with one another in the way I wanted them to. 
My brother-in-law recommended me to look at [Xiaomi's Smart Home](https://xiaomi-mi.com/mi-smart-home/) ecossystem, which, even though amazing, cheap. and with lots of devices, it couldn't communicate with my other devices due to their lack of connection to Xiaomi's Hub. I didn't want to replace them, since I already invested money in them, so I looked for another solution. This is when I encountered [Home Assistant](https://www.home-assistant.io/).

### 1.2. Finding Home Assistant
[Home Assistant](https://www.home-assistant.io/) is an intermediary system that serves, pretty much, as a hub to all your configured devices. It runs on a local server (in my case a [Raspberry Pi 3 Model B+](http://a.co/ak2SQor) with 16GB of SD card memory) and allows for a very nifty database that saves my data locally, hence not requiring my data to be saved to the cloud. Home Assistant provides so many components that it's rare for you to own a device that is not compatible with its system. And even if you manage to get one of those, you can always code, with some trial and error, your own adapter to integrate it into your ecosystem. It isn't necessarily the most straightforward environment, you require lots of tinkering and configuration to get everything up and running, but it's very rewarding to do so. Even if you have no background in programming, or informatics in general, the community has loads of tutorials and it always eager to help you through your journey. 
When I found this I was thrilled: I could re-use all my devices and use the Xiaomi's smart home ecossystem while I was at it, and create a smart home system I was happy with.

----

## 2. Objectives
First, what I had to do was to define core sections that I should primarily focus on, and from them, submerge into their related systems. These are the core sections I decided on:
> - **Comfort** - *the less I do the better*
> - **Security** - *the less I worry  the better*
> - **Control** - *the more I costumize the better*
> - **Feedback** - *the more I know the better*

With these I can list possible systems I will eventually need to work on, and which devices I would need.

| Section     | Systems                                                            | Devices |
|-------------|--------------------------------------------------------------------|---------|
| **Comfort** | automated lights and switches, automated scenes and modes depending on context   | bulbs, LEDs, power switches, motion sensors, climate sensors |
| **Security** | surveillance, door & window state detection, alarms, online security | cameras, climate sensors, door sensors, presence sensors |
| **Control** | family tracking, media control, voice input, external information  (forecasts and traffic), internal and external access | speakers, tvs, routers, natural language processors, device trackers, chromecasts
| **Feedback** | push notifications, speaker TTS, web interfaces | speakers, smartphones, computers|


----
## 3. Devices
Before the showcase of what I have done, here's a table of devices I currently own:
|Device Name | Device | Type | Features | Quantity 
|--|--|--|--|--|
| [Yeelight YLDP02YL](https://pt.gearbest.com/smart-lighting/pp_361555.html) |![Yeelight YLDP02YL](https://gloimg.gbtcdn.com/soa/gb/pdm-product-pic/Electronic/2018/06/20/source-img/20180620161236_33995.jpg =150x)  | **Light** | RGBW, brightness, temperature | 3x
| [Sparin LSP-SmartBulb](https://www.amazon.co.uk/SPARIN-Changing-Compatible-Dimmable-Control/dp/B078N88W1S) | ![Sparin LSP-SmartBulb](https://images-na.ssl-images-amazon.com/images/I/71aM2Kyzj3L._SX522_.jpg =150x) | **Light** | RGBW, brightness, temperature | 7x
| [Bawoo LED Strip](https://www.amazon.es/gp/product/B078SNWRS4/ref=oh_aui_detailpage_o02_s00?ie=UTF8&psc=1) | ![Bawoo LED Strip](https://images-na.ssl-images-amazon.com/images/I/71LKSomFReL._SX466_.jpg =150x) | **Light** | RGBW, brightness, temperature | 2x
| [Amazon Echo Dot 2nd Gen](https://www.amazon.com/Echo-Dot-International-Version-Black/dp/B075RQDJT1/ref=sr_1_5?ie=UTF8&qid=1542852668&sr=8-5&keywords=amazon%20echo%20dot%202nd) | ![Amazon Echo Dot 2nd Gen](https://images-na.ssl-images-amazon.com/images/I/41iz5Tw82IL._SY300_QL70_.jpg =150x) | **Speaker**, **NLU** | voice input, TTS output, speaker | 1x
| [Amazon Echo (2nd Gen)](https://www.amazon.com/Echo-2nd-Generation-International-Version/dp/B075RSCZHD/ref=sr_1_7?s=amazon-devices&ie=UTF8&qid=1542852689&sr=1-7&keywords=amazon%20echo) | ![Amazon Echo (2nd Gen)](https://images-na.ssl-images-amazon.com/images/I/51TFnR7AtGL._SY300_QL70_.jpg =150x) | **Speaker**, **NLU** | voice input, TTS output, speaker | 1x
| [Coosa Smart Socket](https://www.amazon.co.uk/Intelligent-Charger-Compatible-Control-anywhere/dp/B075V47HHP) | ![Coosa Smart Socket](https://images-na.ssl-images-amazon.com/images/I/51GiHELZIKL._SY450_.jpg =150x) | **Switch** | turn on/off power | 3x
| [Xiaomi Aqara Temperature Sensor](https://pt.gearbest.com/access-control/pp_626702.html?wid=1451237) | ![Xiaomi Aqara Temperature Sensor](https://c.76.my/Malaysia/xiaomi-aqara-smart-home-temperature-humidity-pressure-sensor-zigbee-visiongadgetry-1711-14-F612131_1.jpg =150x) | **Sensor** | temperature, humidity, pressure | 2x
| [Xiaomi Aqara Human Sensor](https://pt.gearbest.com/alarm-systems/pp_659226.html?wid=1451237) | ![Xiaomi Aqara Human Sensor](https://gloimg.gbtcdn.com/soa/gb/pdm-product-pic/Electronic/2018/06/21/goods-img/1529546217296309985.jpg =150x) | **Sensor** | motion, luminosity | 4x
| [Xiaomi Aqara Door/Window Sensor](https://pt.gearbest.com/alarm-systems/pp_009129108813.html?wid=1433363) | ![Xiaomi Aqara Door/Window Sensor](https://diyprojects.io/wp-content/uploads/2018/09/100xiaomi-door-window-sensor-pocket-size-xiaomi-smart-home-kits-alarm-system.jpg =150x) | **Sensor** | door opened/closed | 2x
| [Xiaomi Aqara Gateway](https://pt.gearbest.com/living-appliances/pp_344667.html?wid=1433363) | ![Xiaomi Aqara Hub](https://ke.jumia.is/yNdT0w8k0BJ4CP8i9CM_oKbpWco=/fit-in/500x500/filters:fill%28white%29:sharpen%281,0,false%29:quality%28100%29/product/22/43689/1.jpg?9182 =150x) | **Hub**, **Light** | sensor hub, RGBW, brightness, temperature | 1x
| [Xiaomi Aqara Wall Switch Wireless](https://pt.gearbest.com/access-control/pp_626696.html?wid=1451237) | ![Xiaomi Aqara Wall Switch Wireless](https://image4.geekbuying.com/ggo_pic/2017-08-30/Xiaomi-Aqara-Wireless-Wall-Switch-Single-key-Control-White-442782-.jpg =150x) | **Button** | press button | 2x
| [Xiaomi Aqara Wall Switch (Double button) Wireless](https://pt.gearbest.com/alarm-systems/pp_610095.html?wid=1451237) | ![Xiaomi Aqara Wall Switch (Double button) Wireless](https://ae01.alicdn.com/kf/HTB1nkYhc6bguuRkHFrdq6z.LFXa0/2018-Xiaomi-Aqara-Upgrade-Wireless-Switch-Double-Button-Key-Smart-Light-Control-ZigBee-Version-for-Mi.jpg_640x640.jpg =150x) | **Button** | left press, right press, both pressed | 1x
| [Xiaomi Aqara Smart Switch](https://www.aliexpress.com/item/Original-Xiaomi-Smart-Wireless-Switch-for-xiaomi-Smart-Home-House-Control-Center-Intelligent-Multifunction-White-Switch/32801172560.html) | ![Xiaomi Aqara Smart Switch](https://ae01.alicdn.com/kf/HTB145fVQXXXXXcQXFXXq6xXFXXXE/Original-Xiaomi-Smart-Wireless-Switch-for-xiaomi-Smart-Home-House-Control-Center-Intelligent-Multifunction-White-Switch.jpg_640x640.jpg =150x) | **Button** | single click, double click, long click, hold | 1x
| [Broadlink RM Pro+ Smart Wi-Fi IR](https://www.amazon.com/BroadLink-Automation-Universal-Compatible-Smartphones/dp/B0742CXGHY/ref=sr_1_3?ie=UTF8&qid=1542852646&sr=8-3&keywords=broadlink%20rm%20pro) | ![Broadlink RM Pro+ Smart Wi-Fi IR](https://img.dxcdn.com/productimages/sku_405073_1.jpg =150x) | **IR/RF Switch** | send IR/RF packets | 1x 
| [Xiaomi Mi Box 4k HDR](https://www.amazon.com/Original-Xiaomi-Box-Streaming-International/dp/B075QD7HRW/ref=sr_1_3?ie=UTF8&qid=1542852915&sr=8-3&keywords=mi%20box%204k) | ![Xiaomi Mi Box 4k HDR](https://www.pcdiga.com/media/catalog/product/cache/1/image/2718f121925249d501c6086d4b8f9401/1/_/1_15_145.jpg =150x) | **TV Box** | chromecast | 1x

--- 
