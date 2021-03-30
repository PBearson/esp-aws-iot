# ESP-AWS-IoT

This project is a fork of esp-aws-iot from Espressif, and it contain several modifications including support of ESP-IDF versions release/v4.2 and release/v4.3. Also, there is native support for ATECC608A TrustCustom, while other chip types (Trust&Go, TrustFlex) are not currently supported.

## About This Project

This project contains a single application for the ESP32, "subscribe-publish", which can be found in the "examples" directory. This example will connect to AWS IoT, authenticate using a private key stored in the ATECC608A, and communicate using MQTT.

## Getting Started

- Installation instructions for ESP-IDF version release/v4.2 are here: https://docs.espressif.com/projects/esp-idf/en/release-v4.2/esp32/get-started/index.html

- Please clone this repository using,
    ```
    git clone --recursive https://github.com/PBearson/esp-aws-iot
    ```

## Provision the ATECC608A

Before you can run the "subscribe-publish" example, you need to provision the ECC608 that is attached to your ESP32 via the I2C protocol. If you have not done so already, please download the [Provision-ECC608](https://github.com/PBearson/Provision-ECC608) project, which will generate a private key in the crypto chip and provide you with a CSR. **Please make sure to save this CSR to a file.**

## AWS IoT

## Configure the Project

## Build and Run
