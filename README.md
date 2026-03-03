# Implementation of Cross-Platform Data Transmission Systems

## A Comparative Study of Wired Serial and Bluetooth Low Energy (BLE) Bridging using nRF5340

**Authors:**\
Bhargav K, Harsha B J\
Department of Electrical Engineering\
Indian Institute of Technology Hyderabad

------------------------------------------------------------------------

## Abstract

This repository presents the design and implementation of a
cross-platform bidirectional data transmission system enabling seamless
telemetry and file exchange between a Linux host and an Android mobile
environment. The study contrasts a baseline wired USB-CDC serial
connection against a wireless embedded bridge implemented using the
Nordic Semiconductor nRF5340 System-on-Chip (SoC).

In the wireless configuration, the nRF5340 operates as a protocol
translator, bridging USB-CDC (ACM) serial data to Bluetooth Low Energy
(BLE) packets via the Nordic UART Service (NUS). To mitigate binary data
corruption caused by UART control character interpretation, a Base64
encoding strategy was integrated, enabling reliable transmission of
images and PDF files with full data integrity.

------------------------------------------------------------------------

## Keywords

Bluetooth Low Energy (BLE), nRF5340, Zephyr RTOS, USB-CDC, Nordic UART
Service, Base64 Encoding, Embedded Systems, Cross-Platform
Communication, IoT Bridging

------------------------------------------------------------------------

## 1. Introduction

Modern embedded systems increasingly require seamless interoperability
between heterogeneous computing platforms. While wired serial
communication offers high throughput and simplicity, wireless protocols
provide mobility and deployment flexibility.

This project implements and evaluates two communication paradigms:

1.  Direct wired USB-CDC (serial) communication\
2.  Wireless BLE-based bridging using the Nordic nRF5340

------------------------------------------------------------------------

## 2. System Architecture

### 2.1 Wired Serial Mode

Linux Host \<-\> USB-CDC \<-\> nRF5340 DK

-   Virtual serial interface (`/dev/ttyACM*`)
-   Baud rate: 115200
-   Low latency
-   High reliability

### 2.2 Wireless BLE Bridging Mode

Linux Host\
↓ USB-CDC\
nRF5340 DK\
↓ BLE (Nordic UART Service)\
Android Device

The nRF5340 performs protocol conversion between UART and BLE NUS.

------------------------------------------------------------------------

## 3. Hardware Requirements

-   Nordic Semiconductor nRF5340 DK\
-   Linux PC (Ubuntu recommended)\
-   Android Smartphone\
-   USB Type-C cable

------------------------------------------------------------------------

## 4. Software Stack

### Host Environment

-   Ubuntu Linux\
-   Zephyr SDK 0.16.1\
-   nRF Connect SDK v3.2.2\
-   west build system\
-   nrfjprog

### Firmware

-   Zephyr RTOS\
-   peripheral_uart sample\
-   Nordic UART Service (NUS)

------------------------------------------------------------------------

## 5. Installation and Setup

### Install Dependencies

``` bash
sudo apt update
sudo apt upgrade -y
sudo apt install --no-install-recommends -y git cmake ninja-build gperf ccache dfu-util device-tree-compiler wget python3-dev python3-pip python3-setuptools python3-tk python3-wheel xz-utils file make gcc gcc-multilib g++-multilib libsdl2-dev
```

### Install West

``` bash
pip3 install --user -U west
export PATH=$PATH:~/.local/bin
```

### Initialize nRF Connect SDK

``` bash
mkdir ~/ncs
cd ~/ncs
west init -m https://github.com/nrfconnect/sdk-nrf --mr v3.2.2
west update
west zephyr-export
```

------------------------------------------------------------------------

## 6. Build and Flash

``` bash
cd ~/ncs
west build -b nrf5340dk/nrf5340/cpuapp nrf/samples/bluetooth/peripheral_uart
west flash
```

------------------------------------------------------------------------

## 7. Binary File Transfer via Base64

### Linux to Android

``` bash
base64 photo.jpg > /dev/ttyACM0
```

### Android to Linux

``` bash
base64 document.pdf | nc 127.0.0.1 9000
```

Base64 increases file size by approximately 33%. BLE throughput is
approximately 10--20 kB/s.

------------------------------------------------------------------------

## 8. Performance Summary

  Parameter    Wired Serial   BLE (NUS)
  ------------ -------------- ---------------
  Throughput   High           \~10--20 kB/s
  Latency      Low            Moderate
  Power        Higher         Low
  Mobility     No             Yes

------------------------------------------------------------------------

## 9. Conclusion

This project demonstrates a robust bidirectional wireless bridging
architecture using the Nordic nRF5340 SoC. While wired communication
provides superior throughput, BLE bridging offers flexibility and
low-power operation suitable for IoT deployments.

The system validates reliable BLE-based serial bridging, binary-safe
file transfer via Base64, and a reproducible Zephyr RTOS workflow.
