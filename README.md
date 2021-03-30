# ESP-AWS-IoT

This project is a fork of esp-aws-iot from Espressif, and it contain several modifications including support of ESP-IDF versions release/v4.2 and release/v4.3. Also, there is native support for ATECC608A TrustCustom, while other chip types (Trust&Go, TrustFlex) are not currently supported.


## Getting Started

- Installation instructions for ESP-IDF version release/v4.2 are here: https://docs.espressif.com/projects/esp-idf/en/release-v4.2/esp32/get-started/index.html

- Please clone this repository using,
    ```
    git clone --recursive https://github.com/PBearson/esp-aws-iot
    ```
    
## About This Project

This project contains a single application for the ESP32, "subscribe-publish", which can be found in the "examples" directory. This example will connect to AWS IoT, authenticate using a private key stored in the ATECC608A, and communicate using MQTT.

One of the components to this project is the [esp-cryptoauthlib](https://github.com/PBearson/esp-cryptoauthlib/tree/master) submodule, which has been forked from Espressif and updated to support Python 3.8 (the default for recent ESP-IDF releases). This submodule also contains a utility for provisioning the ECC608.

## Provision the ATECC608A

TODO
