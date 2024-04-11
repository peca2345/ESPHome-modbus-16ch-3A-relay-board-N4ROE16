# RS485 16CH 3A Realy Board - Modbus RTU

## Description:
This guide describes how to communicate with ESP MCU using ESPHome for integration into Home Assistant. This solution allows controlling a 16-channel relay board using Home Assistant and the Modbus RTU protocol.

## Info:
- 16ch relay board
- RS485 Modbus RTU
- 12V or 24V version
- max. current 3A/250VAC 3A/30VDC
- DIN rail
- price 28$
- the device does not have a DIP switch for changing the address (only software change of address through PC or ESPHome)
  
## Components:
- 16CH RS485 Relay Board N4ROE16: [ALI](https://www.aliexpress.us/item/3256805729272932.html?spm=a2g0o.order_list.order_list_main.39.2b4f1802Mfl4l0&gatewayAdapt=glo2usa4itemAdapt#nav-specification) / [ELETECH](https://485io.com/rs485-relays-c-2_3_19/n4roe16-mini-dc-24v-16ch-multifunction-modbus-rtu-rs485-relay-board-2a-02w-low-power-consumption-micro-voice-relay-module-n4rof32-p-1015.html) 
- Kincony A4S / A8S / E16S or any ESP with RS485/TTL converter [ALI Kincony A2](https://www.aliexpress.com/item/1005005385355462.html?spm=a2g0o.productlist.main.11.5576hdzNhdzNcU&algo_pvid=3749b2c9-6c7a-4d9c-b7b3-beb28819dd9f&algo_exp_id=3749b2c9-6c7a-4d9c-b7b3-beb28819dd9f-5&pdp_npi=4%40dis%21USD%2153.62%2153.62%21%21%2153.62%2153.62%21%40210388c917128644863171882ea720%2112000032837637725%21sea%21CZ%21166466096%21&curPageLogUid=5cCpVpBKg0a9&utparam-url=scene%3Asearch%7Cquery_from%3A)
- RS485/TTL converter (better) [ALI](https://www.aliexpress.com/item/4001183401209.html?fbclid=IwAR26adPvbd5XSLpuhDKlmJ9YXi_KyOS-wdXoYRxBGDR4IJyzURRGOYdQwMk) (without flow pin!)  

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
    name: "rs485_relay1"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 0
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay2
    name: "rs485_relay2"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 1
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay3
    name: "rs485_relay3"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 2
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay4
    name: "rs485_relay4"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 3
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay5
    name: "rs485_relay5"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 4
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay6
    name: "rs485_relay6"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 5
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay7
    name: "rs485_relay7"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 6
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay8
    name: "rs485_relay8"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 7
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay9
    name: "rs485_relay9"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 8
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay10
    name: "rs485_relay10"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 9
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay11
    name: "rs485_relay11"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 10
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay12
    name: "rs485_relay12"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 11
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay13
    name: "rs485_relay13"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 12
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay14
    name: "rs485_relay14"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 13
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay15
    name: "rs485_relay15"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 14
    bitmask: 1
  - platform: modbus_controller
    modbus_controller_id: relay_board
    id: rs_relay16
    name: "rs485_relay16"
    restore_mode: RESTORE_DEFAULT_OFF
    register_type: coil
    address: 15
    bitmask: 1
```

## Change modbus address:
- To change the address, add the following "on_boot" section
- Edit the current and target device addresses in hex (decimal should also work)
- After uploading the program to the ESP, disconnect the power for 5s and turn it back on
- Now comment out / remove the "on_boot" config from the program and change the address of the modbus_controller to the new address you chose in the "on_boot" config
- Perform the program update again and the device should now work with the new address
```
esphome:
  name: a4s-N4ROE16
  friendly_name: a4s-N4ROE16
## ON BOOT - CHANGE MODBUS ADDRESS "1" to "71"
on_boot:
  priority: -100
  then:
    - lambda: |-
        auto new_address = 0x47;  // New address is 0x47 (71 in decimal)

        if(new_address < 0x01 || new_address > 0xF7) { // Check address range
          ESP_LOGE("ModbusLambda", "Address needs to be between 0x01 and 0xF7");
          return;
        }

        esphome::modbus_controller::ModbusController *controller = id(relay_board);
        auto set_addr_cmd = esphome::modbus_controller::ModbusCommandItem::create_write_single_command(
          controller, 0x00FD, new_address);  // Command to change address

        delay(200);  // Short pause before sending command
        controller->queue_command(set_addr_cmd);
        ESP_LOGI("ModbusLambda", "Meter Addr set to 0x47");
        
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
```
