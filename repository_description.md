# ESPHome Custom Component for AUX Air Conditioners

## Overview

This repository contains a custom component for ESPHome that allows you to control air conditioners manufactured by AUX and other brands produced at AUX factories via Wi-Fi. The component provides comprehensive control over various aspects of compatible air conditioning units through the ESPHome ecosystem.

## Supported Brands

The component works with air conditioners from the following brands that utilize AUX-based technology:
- AUX
- Abion
- AC ELECTRIC
- Almacom
- Ballu
- Centek
- Climer
- DAX
- Energolux
- ERISSON
- Green Energy
- Hyundai
- IGC
- Kentatsu (certain series)
- Klimaire
- KOMANCHI
- LANZKRAFT
- LEBERG
- LGen
- Monroe
- Neoclima
- NEOLINE
- One Air
- Pioneer (up to 2016)
- Roda
- Rovex
- Royal Clima
- SAKATA
- Samurai
- SATURN
- Scarlett
- SmartWay
- Soling
- Subtropic
- SUBTROPIC
- Supra
- Timberk
- Vertex
- Zanussi

## Compatible Models

The repository includes a list of tested and confirmed compatible air conditioner models. These are units that have been successfully controlled using the component by the author or community members. If your air conditioner brand appears in the supported list above, there's a good chance it will work with this component.

## Features

The component supports controlling:
- Operating modes (Heat/Cool, Cool, Heat, Dry, Fan Only)
- Temperature settings
- Fan speeds
- Swing modes (Vertical, Horizontal, Both)
- Special functions like Sleep, Clean, Health, Antifungus
- Display on/off control
- Indoor temperature monitoring

## Hardware Requirements

To use this component, you'll need:
- An ESP8266 or ESP32 microcontroller
- A connection to the UART interface of your air conditioner
- Appropriate wiring and circuitry to connect the ESP to the AC unit

## Software Requirements

- ESPHome version 1.18.0 or higher (preferably 1.20.4 or later due to bug fixes in external components mechanism)

## Installation

1. Add the component to your ESPHome configuration:
   ```yaml
   external_components:
     - source:
         type: git
         url: https://github.com/GrKoR/esphome_aux_ac_component
   ```

2. Configure UART for communication with your air conditioner:
   ```yaml
   uart:
     id: ac_uart_bus
     tx_pin: GPIO1
     rx_pin: GPIO3
     baud_rate: 4800
     data_bits: 8
     parity: EVEN
     stop_bits: 1
   ```

3. Disable the ESPHome logger to prevent interference:
   ```yaml
   logger:
       baud_rate: 0
   ```

## Basic Configuration

```yaml
climate:
  - platform: aux_ac
    name: "AC Name"
```

## Full Configuration Example

```yaml
climate:
  - platform: aux_ac
    name: "AC Name"
    id: aux_id
    uart_id: ac_uart_bus
    period: 7s
    show_action: true
    indoor_temperature:
      name: AC Indoor Temperature
      id: ac_indoor_temp
      internal: true
    display_state:
      name: AC Display
      id: ac_display
      internal: false
    visual:
      min_temperature: 16
      max_temperature: 32
      temperature_step: 0.5
    supported_modes:
      - HEAT_COOL
      - COOL
      - HEAT
      - DRY
      - FAN_ONLY
    custom_fan_modes:
      - MUTE
      - TURBO
    supported_presets:
      - SLEEP
    custom_presets:
      - CLEAN
      - FEEL
      - HEALTH
      - ANTIFUNGUS
    supported_swing_modes:
      - VERTICAL
      - HORIZONTAL
      - BOTH
```

## Additional Actions

The component provides special actions for display control:
- `aux_ac.display_on`: Turns on the temperature display on the air conditioner panel
- `aux_ac.display_off`: Turns off the temperature display on the air conditioner panel

## Examples

The repository includes both simple and advanced examples showing how to configure the component for different use cases.

## Community and Support

For discussion and support, join the Telegram chat linked in the original repository. Bug reports, feature requests, and compatibility reports are welcome in the issues section.

## Disclaimer

All materials in this project are provided "as is". Users are responsible for their own equipment and modifications. The author makes no warranties and assumes no liability for the results of using this software.

## Contributing

If you've tested a model not listed in the compatible devices list, please share your findings to help expand the database of supported units.