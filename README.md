# Bean Butler – firmware & Home Assistant files

| File | What it is |
|---|---|
| `bean-butler.yaml` | ESPHome firmware for the ESP32-2432S028 (Guition V1.3) |
| `bean-butler/waving.gif`, `sleeping.gif`, `rinsing.gif` | Display animations – put them in `/config/esphome/bean-butler/` |
| `secrets.example.yaml` | The secrets the firmware needs – copy the entries into your ESPHome `secrets.yaml` |
| `remote_coffee_script.yaml` | HA script "Remote coffee": divert rinse, power on, wait, coffee |
| `follow_machine_automation.yaml` | Optional HA automation: display and channel follow the machine |

## Setup in short

1. **ESPHome:** create a new device "bean-butler", replace its YAML with `bean-butler.yaml`,
   copy the GIFs and add the secrets. Change the entity IDs under `substitutions` to your coffee machine.
2. **First flash via USB** (power supply disconnected!), later updates over Wi-Fi.
3. **Add the device in Home Assistant.** You get e.g. `switch.bean_butler_divert_rinse`,
   `light.bean_butler_display_brightness` and the two angle settings.
4. **Mount the hub:** don't turn the servo shaft by hand. Switch "Divert rinse" on, then push the hub on so the
   channel sits under both spouts. Fine-tune with "Channel angle divert" / "Channel angle open".
5. **Add the script** (and optionally the automation) and replace the entities marked `CHANGE`.

## Requirements

- Home Assistant with ESPHome
- A coffee machine that HA can power on and start a coffee on. Built and tested with a De'Longhi machine
  and the `delonghi_coffeelink` integration. Other integrations may report different
  status values – adjust them in the firmware and the script.

## Known quirks

- **White screen?** ESPHome 2026.x has an issue with CYD displays. The firmware uses `mipi_spi` / `ILI9341`
  without `miso_pin` on the display SPI, `data_rate: 20MHz` – keep it that way.
- **Servo hums or clicks constantly:** the channel is pushing against something. Power off and check the angles.
- The machine also rinses when it **powers off** – a cup left underneath will catch that.

License: CC BY-NC-SA 4.0
