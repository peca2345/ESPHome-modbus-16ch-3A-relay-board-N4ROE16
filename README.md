# ESPHome - 16CH 3A Realy Board RS485 Modbus RTU

## Info:
- 16ch 3A relay board RS485 Modbus RTU

## Components:
- 16CH RS485 Relay Board N4ROE16: [ALI](https://www.aliexpress.us/item/3256805729272932.html?spm=a2g0o.order_list.order_list_main.39.2b4f1802Mfl4l0&gatewayAdapt=glo2usa4itemAdapt#nav-specification) / [ELETECH](https://485io.com/rs485-relays-c-2_3_19/n4roe16-mini-dc-24v-16ch-multifunction-modbus-rtu-rs485-relay-board-2a-02w-low-power-consumption-micro-voice-relay-module-n4rof32-p-1015.html) 
- Kincony A4S / A8S / E16S or any ESP with RS485/TTL converter. [ALI Kincony A2](https://de.aliexpress.com/item/1005005385355462.html?spm=a2g0o.productlist.main.9.2a7979888Tsesu&algo_pvid=022308dc-819a-4ed5-9940-b5636d6bf2c5&algo_exp_id=022308dc-819a-4ed5-9940-b5636d6bf2c5-4&pdp_npi=4%40dis%21USD%2153.62%2153.62%21%21%2153.62%2153.62%21%402101dee017128618204757036e06d6%2112000032837637725%21sea%21CZ%21166466096%21&curPageLogUid=s5qWmPFoNffs&utparam-url=scene%3Asearch%7Cquery_from%3A)
- RS485/TTL converter (better): [SHOP](https://www.aliexpress.com/item/4001183401209.html?fbclid=IwAR26adPvbd5XSLpuhDKlmJ9YXi_KyOS-wdXoYRxBGDR4IJyzURRGOYdQwMk) (without flow pin)  

## Datasheet:
- Manual: [N4ROE16](https://github.com/peca2345/ESPHome-modbus-16ch-3A-relay-board-N4ROE16/blob/main/DATA/N4ROE16%20Manual.pdf)
- Modbus: [N4ROE16](https://github.com/peca2345/ESPHome-modbus-16ch-3A-relay-board-N4ROE16/blob/main/DATA/N4ROE16%20MODBUS%20RTU%20Commamd.pdf)
- Software: [N4ROE16](https://github.com/peca2345/ESPHome-modbus-16ch-3A-relay-board-N4ROE16/blob/main/DATA/N4ROA01_N4ROB02_N4ROC04_N4ROD08_N4ROE16_N4ROF32%20Manual.rar)
  
## Home Assistant Dashboard:
![DSM630MCT](https://github.com/peca2345/ESPHome-modbus-16ch-3A-relay-board-N4ROE16/blob/a0e2a1e382621f528fbd987088412eff6d14c310/DATA/HA.png)

## Wiring:
![Wiring](https://github.com/peca2345/ESPHome-modbus-16ch-3A-relay-board-N4ROE16/blob/a0e2a1e382621f528fbd987088412eff6d14c310/DATA/test.png)

## Modbus RTU Function Codes:
![function codes](https://github.com/peca2345/ESPHome-modbus-16ch-3A-relay-board-N4ROE16/blob/main/DATA/rs485_function_code.png?raw=true)

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

