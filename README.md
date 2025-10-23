# ESPHome Configuration Templates

This repository provides a collection of modular ESPHome configuration templates for various microcontroller boards and sensors. The templates are designed to be easily customizable and maintainable using ESPHome's package system.

## Purpose

This repository serves as a centralized collection of:
- **Base configurations** for popular development boards (ESP32, ESP32-C3, ...)
- **Modular addons** for common sensors and features (Bluetooth, motion detection, etc.)
- **Interface configurations** for communication protocols (I2C)
- **Ready-to-use templates** that combine these components for specific use cases

## Quick Start

The templates in the `templates/` directory are ready to be used directly in ESPHome. Each template pulls configurations from this repository using ESPHome's package system, making updates and maintenance seamless.

### Available Templates

- **ESP32 Dev board** (`templates/esp32-dev.yaml`) - Vanilla board for ESP32.
- **ESP32-C3 Mini board** (`templates/esp32-c3-mini.yaml`) - Vanilla board for ESP32-C3.

## Repository Structure

```
├── base/           # Base board configurations
├── interface/      # Communication interface configs (I2C, etc.)
├── addon/          # Modular feature addons
└── templates/      # Ready-to-use device templates
```

### Modular Design

The configurations are split into modular components:

- **Base**: Core board setup (pins, basic functionality)
- **Interface**: Communication protocols and pin mappings
- **Addons**: Specific sensors and features that can be mixed and matched
- **Templates**: Pre-configured combinations for common use cases

## Getting Started with ESPHome

If you're new to ESPHome, check out the [official documentation](https://esphome.io/) to learn more about this powerful framework for microcontroller programming.

## Support

For ESPHome-specific questions, refer to the [ESPHome documentation](https://esphome.io/) and [community forums](https://community.home-assistant.io/c/esphome).

---

**Happy coding!** 🚀 Fork this repository and make it your own! This version was based on https://github.com/jtenniswood/esphome repository.
