---
title: "Sensor Setup"
date: 2022-09-16T12:31:17+01:00
draft: false
---
# Configuration

In this section, the required programs for connecting your ESP board to gcloud are mentioned and how to properly download these programs for Win10 or macOS. This tutorial is aimed to people with little to no experience programing microcontrollers.

## Required Programs
The programs that you need to download in order to follow this tutorial are the following:
- Arduino IDE
- Google Cloud CLI
- Git-Bash (for Windows 10 users)
- Python (can be installed when installing the Google Cloud CLI --preferred)
- The program corresponding to the sensor type you want to use found [HERE](https://github.com/opencell-community) 
- Board driver

## Installing the Required Programs
### Arduino IDE
1. Go to [arduino.cc/en/software](https://www.arduino.cc/en/software) 
2. Click on your operating system and version under “Download Options”.
3. Click on the “Just Download” button (unless you would like to donate to the company).
4. Save the installer executable then run it. 
5. Accept any permissions requirements.
6. Follow the installer’s instructions. 
> **NOTE:** Make sure to select the USB driver component and associated .ino files
7. Open the program and go to Tools > Manage Libraries. The following window will pop up:
> INSERT IMAGE 1
8. Install the following libraries (by typing into the  _Filter your Search_ box):
	1. **ArduinoJson** (by Benoit Blanchon, version 6.19.1)
	2. **DHT Sensor Library** (by Adafruit, version 1.4.3) --with all the missing dependencies
	3. **Google Cloud IoT Core JWT** (by Gus Class, version 1.1.11)
	4. **MQTT** (by Joel Gaehwiler, version 2.5.0)
	5. **OneWire** (by Paul Stoffregen, version 2.3.7)
	6. **DallasTemperature** (by Miles Burton, version 3.9.0)
	7. **base64** (by Densaugeo, version 3.9.0)
	8. **WiFiManager** (by tablatronix, version 2.0.11-beta)
	9. **Adafruit_MAX31855** (by Adafruit, version 1.0.4)
9. Close the Library Manager
10. Go to Tools > Board > Boards Manager and install “ESP8266” boards (by ESP8266 Community, version 3.0.2). Close the window.
> If the board does not appear here, go to File (‘Arduino’ on OS) > Preferences > Additional Boards Manager URLs and paste:
> 
>`https://dl.espressif.com/dl/package_esp32_index.json,   http://arduino.esp8266.com/stable/package_esp8266com_index.json`  
>
> Then, try step #10 again. This takes a few minutes.

11. Go to Tools > Board > ESP8266 Boards (3.0.2) and select the _LOLIN(WEMOS) D1 R2 & Mini_ board.
> INSERT IMAGE 2
### Google Cloud CLI
1. Go to [cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install).
2. Click on “download and install the `gcloud cli`”.
3. Select your corresponding operating system and download the installer:
4. Configure and login to the google cloud CLI and have an account registered with the necessary permissions to register new IOT devices.

## Device setup & configuration

To install a new sensor: 
 - configure your user with `gcloud auth login`
 - run registerdevice.sh through the command line `./registerdevice.sh <MY_SENSOR_NAME>`
 - compile the firmware with the Arduino IDE   
 - Upload to device
 - Check the device is working correctly by reading the COM port in the arduino IDE serial monitor 

## Concepts

The IOT sensors wake periodically, collect sensors readings then send via HTTP to the IOT gateway.

To save power the boards go into the ESP8266 deep sleep mode after collecting and transmitting the data.

Once a board has been registered, it will create a temporary wifi hotspot and captive portal to configure the network and password. Once correctly entered it will save these credentials and some other data about the wifi connection to the rtc memory of the board.

Based on a private key written into the board software and also mirrored to the IOT gateway, the device creates a signed JWT locally to authenticate requests. This is generated only on device boot and is refreshed only once it expires to save the battery life necessary to compute the JWT afresh each time.

The RTC memory code uses CRC32 checksums to ensure data integrity across power cycles.

Some branches of the code exist which store consecutive sensor readings in adjacent sectors of the RTC memory to allow the board to wake periodically, fill a buffer with readings then transmit them all in one go. E.g take 5 readings at 1 minute intervals but only send them once every 5 minutes.(RTC memory has approx 512 addressable bytes)

Power consumption is greatest when using the radio, so further development should be mindful of only sending and receiving data when it is absolutely necessary.




