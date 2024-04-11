# ESPHome - 16CH 3A Realy Board RS485 Modbus RTU

## Description:
It is a three-phase non-invasive wattmeter with a DIN rail measuring coil. It communicates via modbus protocol via ESP8266/ESP32 to LAN. The program is written using ESPHome and is fully integrated into Home Assistant. It is a cheap alternative to, for example Shelly 3EM.

![DSM630MCT](https://github.com/peca2345/ESPHome-modbus-wattmeter-DSM630MCT/blob/main/IMG/DSM630MCT_rs485.png?raw=true)

![Lovelace](https://github.com/peca2345/ESPHome-modbus-wattmeter-DSM630MCT/blob/main/IMG/lovelace2.png?raw=true)

## Info:
- modbus datasheet: [DSM630MCT](https://github.com/peca2345/ESPHome-modbus-wattmeter-DSM630MCT/blob/main/IMG/DSM630MCT_3_phase_wattmeter_datasheet.pdf)
- I do not recommend buying an unnecessary large clamp - 100A is really huge!
- on the wattmeter you have to set the transformer type to make an accurate measurement
- use only shielded cable, otherwise the error "Modbus CRC Check Failed!" may appear in the log.
- put a 120 ohm resistor after the last connected device
- you have to find out what the wattmeter address is - default is 0x01
- you also need to find out the serial port speed - default 9600
- in ESPHome use the sensor class only for addresses that are read-only
- for addresses that are read use the "sensor" class
- for addresses that are write use the "number" class (you can then change their values in lovelace)
- for each register you want to have in HA you have to create a separate sensor in ESPHome
- as long as the address of the device is the same as some sensor, it doesn't matter
- wattmeter works with default address 0x01

## Components:
- ESP8266 / ESP32
- RS485/TTL converter: [SHOP](https://www.laskakit.cz/prevodnik-ttl-na-rs-485--max485/) (not very good quality, interference occurs)  
- RS485/TTL converter (better): [SHOP](https://www.aliexpress.com/item/4001183401209.html?fbclid=IwAR26adPvbd5XSLpuhDKlmJ9YXi_KyOS-wdXoYRxBGDR4IJyzURRGOYdQwMk) (without flow pin)  
- Wattmeter DSM630MCT: [SHOP](https://www.aliexpress.com/item/1005004059758839.html?dp=60884bf2d2ed5efc7c969b20&cn=ah&aff_fcid=f70ab32472014c52a8e7cedd4dd3921e-1682023557871-06550-_sSETun&aff_fsk=_sSETun&aff_platform=link-c-tool&sk=_sSETun&aff_trace_key=f70ab32472014c52a8e7cedd4dd3921e-1682023557871-06550-_sSETun&terminal_id=153e61cce3cb4f32a9ecb3735d8d5ed6&afSmartRedirect=y) 

## Schematic ESP32:
![Schema](https://github.com/peca2345/ESPHome-modbus-wattmeter-DSM630MCT/blob/main/IMG/schematic2.png?raw=true)

## Schematic ESP8266 - Wemos D1 mini:
![Schema](https://github.com/peca2345/ESPHome-modbus-wattmeter-DSM630MCT/blob/main/IMG/schematic_wemos.png?raw=true)

## Wiring:
![Wiring](https://github.com/peca2345/ESPHome-modbus-wattmeter-DSM630MCT/blob/main/IMG/schema.jpg?raw=true)

## Transformer size setting:
![settings](https://github.com/peca2345/ESPHome-modbus-wattmeter-DSM630MCT/blob/main/IMG/settings.png?raw=true)


## Modbus address:
```
0x01  Wattmeter default address
```

```
0x00  A-phase voltage         XXX.X V 
0x01  B-phase voltage         XXX.X_V 
0x02  C-phase voltage         XXX.X V 
0x03  A phase current         XXX.X A 
0x04  B phase current         XXX.X A 
0x05  C phase current         XXX.X A 
0x06  Neutral current         XXX.X A

```
## ESPHome code:
```
esphome:
  name: a4s-N4ROE16
  friendly_name: a4s-N4ROE16

esp32:
  board: esp32dev
  framework:
    type: arduino

logger:

api:
  encryption:
    key: "R86/CjUd0rIfghfxghfsgjsfjsfdgjsfgj415lu/y97FMHCt3F0="

ota:
  password: "4h56r454j56fgd4j5fg6j4fg56dj1fgdj"

wifi: 
  ssid: !secret wifi_ssid
  password: !secret wifi_password

captive_portal:
    
######################### 
    
uart:
  id: mod_bus
  rx_pin: GPIO33
  tx_pin: GPIO32
  baud_rate: 9600
  stop_bits: 1

modbus:
  send_wait_time: 200ms
  id: rs485

modbus_controller:
  - id: relay_board
    address: 1
    modbus_id: rs485
    setup_priority: -10
    
#########################

switch:
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay1
    name: "Relay 1"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 0
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay2
    name: "Relay 2"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 1
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay3
    name: "Relay 3"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 2
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay4
    name: "Relay 4"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 3
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay5
    name: "Relay 5"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 4
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay6
    name: "Relay 6"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 5
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay7
    name: "Relay 7"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 6
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay8
    name: "Relay 8"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 7
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay9
    name: "Relay 9"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 8
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay10
    name: "Relay 10"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 9
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay11
    name: "Relay 11"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 10
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay12
    name: "Relay 12"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 11
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay13
    name: "Relay 13"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 12
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay14
    name: "Relay 14"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 13
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay15
    name: "Relay 15"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 14
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay16
    name: "Relay 16"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 15
    bitmask: 1
```

