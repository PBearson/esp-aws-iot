# ESP-AWS-IoT

This project is a fork of esp-aws-iot from Espressif, and it contain several modifications including support of ESP-IDF versions release/v4.2 and release/v4.3. Also, there is native support for ATECC608A TrustCustom, while other chip types (Trust&Go, TrustFlex) are not currently supported.

## About This Project

This project contains a single application for the ESP32, "subscribe-publish", which can be found in the "examples" directory. This example will connect to AWS IoT, authenticate using a private key stored in the ATECC608A, and communicate using MQTT.

## Getting Started

- Installation instructions for ESP-IDF version release/v4.2 are here: https://docs.espressif.com/projects/esp-idf/en/release-v4.2/esp32/get-started/index.html

- Please clone this repository using the following command:
    ```
    git clone --recursive https://github.com/PBearson/esp-aws-iot
    ```

## Provision the ATECC608A

Before you can run the "subscribe-publish" example, you need to provision the ECC608 that is attached to your ESP32 via the I2C protocol. If you have not done so already, please download the [Provision-ECC608](https://github.com/PBearson/Provision-ECC608) project, which will generate a private key in the crypto chip and provide you with a CSR. **Please make sure to save this CSR to a file.**

## AWS IoT

After you have provisioned the ECC608 and saved your CSR to a file, open your AWS IoT console. There you will upload the CSR by going to Secure -> Certificates -> Create -> Create with CSR. AWS will sign the CSR and provide you with a valid device certificate. Download the certificate, and make sure to activate it in the console. You also need to attach a valid IoT policy to your certificate. A sample policy is shown below, which grants full IoT access to authorized devices:

![IoT Policy](iot-policy.JPG)

## Configure the Project

Navigate to the "subscribe-publish" directory:

```
cd esp-aws-iot/examples/subscribe_publish
```

Place the downloaded device certificate to the "main/certs" directory. Rename the certificate file to "certificate.pem.crt".

Now open the menu config with the following command:

```
idf.py menuconfig
```
You must configure the following settings to successfully connect your device to AWS IoT:
- Example Configuration -> WiFi SSID
- Example Configuration -> WiFi Password
- Component config -> esp-cryptoauthlib -> Enable Hardware ECDSA keys for mbedTLS
- Component config -> esp-cryptoauthlib -> Enable ATECC608A sign operations in mbedTLS
- Component config -> esp-cryptoauthlib -> Enable ATECC608A verify operations in mbedTLS
- Component config -> esp-cryptoauthlib -> I2C SDA pin used to communicate with the ATECC608A
- Component config -> esp-cryptoauthlib -> I2C SCL pin used to communicate with the ATECC608A
- (OPTIONAL) Component config -> esp-cryptoauthlib -> Scan for ATECC608A I2C
- Component config -> Amazon Web Services IoT Platform -> AWS IoT Endpoint Hostname
- Component config -> Amazon Web Services IoT Platform -> Enable the hardware secure element for authenticating TLS connections

The AWS IoT endpoint can be obtained in the AWS IoT console on the "settings" page.

If "Scan for ATECC608A I2C" is not selected, then the application will try to use address 0xC0 by default.

## Build and Run

To build and flash the app, run the following command:

```
idf.py build flash monitor
```

The ESP32 will attempt to connect to AWS IoT. If the procedure was followed correctly, then the ESP32 will use its device certificate and device private key (stroed in slot 0 of the ECC608) to authenticate to AWS IoT.

Observe the output carefully, as it can give important information regarding any errors that occur. If the ESP32 succeeded in initializing the ECC608, you will see the following output:

![ECC608 initialized](ecc608-initialized-successfully.JPG)
