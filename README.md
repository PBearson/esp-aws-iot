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

Navigate to the esp_cryptoauthlib_utility directory:

```
cd esp-aws-iot/examples/subscribe_publish/components/esp-cryptoauthlib/esp_cryptoauthlib_utility
```

Generate a signer certificate and signer private key:

```
openssl ecparam -out signerkey.pem -name prime256v1 -genkey
openssl req -new -x509 -key signerkey.pem -out signercert.pem -days 365
```

Make sure the the signer certificate's Common Name ends in "FFFF", e.g., "My Cert FFFF".

Install Python dependencies:

```
pip install -r requirements.txt
```

Now run the secure_key_mfg.py script to generate a private key inside slot 0 of ECC608 and generate a device certificate:

```
python secure_cert_mfg.py --signer-cert signercert.pem --signer-cert-private-key signerkey.pem --port <PORT>
```

The device certificate will be printed to the screen, and it will also be saved to a new "output_files/" directory.
