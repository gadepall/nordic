# BLE HID Keyboard Bridge using nRF5340

This project demonstrates how a Nordic nRF5340 development board can be used as a bridge to transmit keyboard input from one Linux laptop to another using Bluetooth Low Energy (BLE).

The system works by receiving ASCII characters over a UART serial connection and converting them into HID keycodes that are transmitted through the BLE HID Keyboard profile.

---

## System Overview

The architecture of the system is as follows:

Laptop A (Keyboard Input)  
↓  
Serial Terminal (`screen`)  
↓  
USB UART → nRF5340  
↓  
ASCII → HID Conversion  
↓  
BLE HID Keyboard  
↓  
Laptop B (Receives keystrokes)

Characters typed on the transmitting laptop are received by the nRF5340 and sent wirelessly as keyboard events to the receiving laptop.

---

## Implementation

Add this main.c code into the src/main.c folder inside peripheral_hids_keyboard folder and then build and flash the code onto the board.
