# emonTx V3.4.x

[![Build Status](https://travis-ci.org/openenergymonitor/emontx3.svg?branch=master)](https://travis-ci.org/openenergymonitor/emontx3)

![photo.jpg](hardware/photo.jpg)

## My Hardware

### emon Tx V3 (£66.30 + VAT)

* Order date 13th Dec 2014
* RF Module: RFM12B 433Mhz
* Node ID : 10 (default)
* Enclosure: Fully Assembled
* Clip-on CT Current Sensor: 1 x 100A Max Clip-on CT Sensor
* AC Power Adapter: Euro Plug

### emonBase - Raspberry Pi web-connected base-station (£17.91+ VAT)

* Order date 13th Dec 2014
* RaspberryPi RF add-on: RFM12Pi - 433MHz

###  3 x 100A max clip-on current sensor CT (3 x £8.00 + VAT)

### Programmer - USB to serial UART (£5.83 + VAT )

* Order date 11th Jan 2015

### RJ45 Encapsulated DS18B20 temperature sensor (£6.80 + VAT )

* Order date 11th Jan 2015

## Other OpenEnergyMonitor Hardware

### 2 x emonTH 433MHz - Temperature & Humidity Node (£32.30 + VAT )

* Order date: Nov - Dec 2015
* Sensor: DTH22 - Temperature & Humdity
* RF node ID (unique per network): 19 (defaut)

### 1 x  Three Channel WiFi MQTT Relay / Thermostat (£43.20 + VAT )

* Order date: 15 Nov 2015
* Power Supply: On-board AC Power Supply
* Sensor: No Sensor

## My Setup

## Hardware

The 3 phases:

* P1 - L1 (phase 1) => no power intensive devices like (dryer, merceded, ...)
* P1 - L2 (phase 2) => zonnepanelen.
* P1 - L3 (phase 3) => Mercedes , droogkast, vaatwasser

The 4 CT sensors

* CT wire 1 - fuse F (brown) - Solar pannels - CT1 
* CT wire 2 - fuse K (blue) - Garage - CT2
* CT wire 3 - fuse I (brown x 2) - dryer/washing machine - CT3 
* CT wire 4 - fuse H (brown) - dish washer... - CT4 

### Software / Firmware

1. My emonTx V3.4 sends power data every 10 seconds via RFM12B at 433 mHz frequency for node 10
   * I have uploaded sketch `emonTx34_DS_jeelib_classic` of this repository
2. which is received by my RFM12PI expansion board on [pi3one](https://github.com/janvda/pi3one).
3. Emonhub on my pi3one is forwarding that data to my MQTT server running on pi3one using topic `emonhub/rx/10/values`
4. This data is also received by my home-assistant MQTT broker running on nuc2 using MQTT bridge functionality
5. home-assistant on nuc2 using MQTT integration connecting to my home assistant MQTT broker is receiving this data.
   * in file `/config/configuration.yaml` of my home-assistant container I have defined the different emon Tx sensor values that are broadcasted to the MQTT server.


see also:

* https://docs.openenergymonitor.org/emontx3/3phase.html

## Uploading (new) firmware

Use arduino app on macbook.

Connected my macbook with emonTx using the `Programmer - USB to serial UART` device and micro USB cable.

see also:
* https://community.openenergymonitor.org/t/would-like-to-upgrade-old-firmware-on-my-emontx-v3-device

## Testing

### MQTT

Using the MQTTX app on my macbook I have setup a connection to my home-assistant MQTT broker on nuc2.  When I then subscribe to `emonhub/#` I see every 10 seconds an `emonhub/rx/10/values` MQTT message listing the 5 values (e.g. `732,-10,-69,14,254`)

## Documentation

- [Overview](https://docs.openenergymonitor.org/emontx3/overview.html)
- [Install Guide](https://docs.openenergymonitor.org/emontx3/install.html)
- [Adding to an existing install](https://docs.openenergymonitor.org/emontx3/add.html)
- [3 phase](https://docs.openenergymonitor.org/emontx3/3phase.html)
- [Add ESP8266](https://docs.openenergymonitor.org/emontx3/esp8266.html)
- [Direct Serial](https://docs.openenergymonitor.org/emontx3/direct.html)
- [Configuration](https://docs.openenergymonitor.org/emontx3/configuration.html)
- [Firmware](https://docs.openenergymonitor.org/emontx3/firmware.html)
- [Technical](https://docs.openenergymonitor.org/emontx3/technical.html)

This documentation can also be viewed on github directly [here](docs).
