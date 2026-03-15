# Nordic nRF5340 Embedded Communication Projects

This repository contains embedded system projects implemented using the **Nordic Semiconductor nRF5340 Development Kit** and the **nRF Connect SDK (Zephyr RTOS)**.

The projects demonstrate how the nRF5340 can be used as a **communication bridge between wired interfaces and Bluetooth Low Energy (BLE)**.

Two main systems were implemented:

1. **BLE UART File Transfer System**
2. **BLE HID Keyboard Bridge**

Both projects were developed and tested on **Linux systems**.

---

# Hardware Used

- Nordic **nRF5340 Development Kit**
- Two Linux laptops
- USB connection to development board

---

# Software Environment

The following tools were used:

- **nRF Connect SDK v3.2.2**
- **Zephyr RTOS**
- **West build system**
- **Zephyr SDK Toolchain**
- **nRF Command Line Tools**

---

# Project 1 — BLE UART File Transfer

## Overview

This project demonstrates **wireless file transfer using Bluetooth Low Energy** by utilizing the **Nordic UART Service (NUS)**.

The nRF5340 board acts as a **bridge between USB serial communication and BLE**.

Data sent over USB serial is transmitted over BLE and received on another device.

---

# Project 2 — BLE HID Keyboard Bridge

## Overview

This project converts the nRF5340 development board into a **Bluetooth Low Energy keyboard device** using the BLE Human Interface Device (HID) profile.

Keyboard input from one Linux laptop is transmitted to another Linux laptop through the nRF5340 board. The transmitting laptop sends characters over a **USB serial interface**, which are received by the nRF5340. The firmware converts the received ASCII characters into **HID keycodes** and sends them wirelessly to the receiving laptop via BLE.

As a result, the receiving laptop interprets the nRF5340 as a **standard Bluetooth keyboard**.

---

## License

This project is based on sample code from the Nordic nRF Connect SDK.

The original sample code is licensed under the Nordic 5-Clause License.

All additional modifications and documentation in this repository were developed for academic purposes.

