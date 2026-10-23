# ESPHome Projects

Modular [ESPHome](https://esphome.io/) configs: board bases, addons to mix and match, and the device configs built from them. Devices pull these files straight from this repository with ESPHome's [package system](https://esphome.io/components/packages/), so a change here reaches every device on its next build.

Each base sets the oldest ESPHome version it builds with (`min_version`).

## Repository Structure

```
├── base/          # Board configs, each with the addons every device on that board gets
├── addon/         # Features: logging, OTA, buttons, Bluetooth, status LED, time window, ...
│   ├── io/        # Hardware: camera, I2C, PSRAM, CW/WW light and its Halloween effects, MAX98357A speaker
│   └── sounds/    # Sound clips, with a select and a button to play them
├── devices/       # Configs for specific devices
├── sounds/        # WAV clips for addon/sounds/
└── templates/     # Starting points for a new device
```

## Boards

| Base | Board | Framework | Adds |
| --- | --- | --- | --- |
| `base/esp32-c3-mini.yaml` | ESP32-C3 | ESP-IDF | Factory reset button |
| `base/esp32-dev.yaml` | ESP32 DevKit | ESP-IDF | Bluetooth tracker and proxy |
| `base/esp32-cam.yaml` | ESP32-CAM | Arduino | Camera and its web server, I2C, PSRAM, factory reset button |

Every base also has logging, OTA, safe mode, a restart button, Home Assistant time, the web server, and the network sensors (Online, Last Boot, Wi-Fi signal and strength, IP, MAC, BSSID, Version).

## Using It

A device config sets the substitutions the base uses, its API key and Wi-Fi, and lists the files it wants:

```yaml
substitutions:
  name: halloween-pumpkin
  friendly_name: Halloween Pumpkin
  area: Kitchen
  project: lights.pumpkin
  version: "1.0"
  frequency: 4800Hz # Used by addon/io/light_cwww.yaml.

api:
  encryption:
    key: !secret encryption_key
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

packages:
  base:
    url: https://github.com/csobrinho/esphome-projects/
    ref: main
    refresh: 1sec # Fetch the latest files on every build.
    files:
      - path: base/esp32-c3-mini.yaml
      - path: addon/io/light_cwww.yaml
        vars: { name: "Pumpkin", dev: "pumpkin", led_cw_pin: GPIO4, led_ww_pin: GPIO3 }
```

- Each addon's header comment lists the `vars` and substitutions it needs.
- Most addons take `dev`, which prefixes the ids they create (`pumpkin_light`), and `name`, which prefixes the entity names ("Pumpkin Light").
- Use `!extend` with an id to add to or change what an addon created.
- `secrets.yaml` needs `encryption_key`, `wifi_ssid` and `wifi_password`.

## Templates

- `templates/esp32-c3-mini.yaml` and `templates/esp32-dev.yaml`: a bare device on that board, with a commented-out CW/WW light to start from.

## Devices

| Config | Board | What it does |
| --- | --- | --- |
| `chime.yaml` | ESP32-C3 | Rings a doorbell chime (left and right, or right only) through two open-drain outputs, with an adjustable pulse length |
| `halloween-pumpkin.yaml` | ESP32-C3 | Carved pumpkin: CW/WW light with Halloween effects, PIR scares, a speaker with sounds, and quiet hours |
| `infra-kvm-switch.yaml` | ESP32-C3 | Switches an HDMI KVM's channel and power over IR |
| `kitchen-lights.yaml` | ESP32 DevKit | Four CW/WW LED strips |
| `lanbo-data-logger.yaml` | ESP32-C3 | Decodes a Lanbo fridge's UART traffic with the `lanbo_decoder` external component, loaded from a local path outside this repo |
| `sink-camera.yaml` | ESP32-CAM | Camera with a flash that's on while streaming |
| `outdoor-floodlights.yaml` | BK7231N (Tuya) | CW/WW floodlight; standalone, uses no files from this repo |
| `ratgdo.yaml` | ratgdo v2.5i | Garage door opener from the upstream [ratgdo](https://github.com/ratgdo/esphome-ratgdo) package |

## Getting Started with ESPHome

If you're new to ESPHome, check out the [official documentation](https://esphome.io/) to learn more about this powerful framework for microcontroller programming.

## Support

For ESPHome-specific questions, refer to the [ESPHome documentation](https://esphome.io/) and [community forums](https://community.home-assistant.io/c/esphome).

---

**Happy coding!** 🚀 Fork this repository and make it your own! This version was based on https://github.com/jtenniswood/esphome repository.
