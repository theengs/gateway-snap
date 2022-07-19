[![theengs-gateway](https://snapcraft.io/theengs-gateway/badge.svg)](https://snapcraft.io/theengs-gateway)

# Theengs Gateway Snap

[Theengs Gateway](https://github.com/theengs/gateway) packaged as a snap.

## How to install

[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-white.svg)](https://snapcraft.io/theengs-gateway)

You can install it on amd64 and arm64 systems as:

```shell
snap install theengs-gateway
```

If you're running this on Ubuntu Core on a Raspberry Pi, also install the following snaps for Bluetooth:

```shell
snap install bluez pi-bluetooth
```

## How to configure

You can show the snap's configuration with:

```shell
$ snap get -d theengs-gateway
{
        "ble": {
                "adapter": "",
                "scan-duration": 5,
                "time-between": 5
        },
        "ha": {
                "discovery": 1,
                "discovery-device-name": "TheengsGateway",
                "discovery-filter": "IBEACON GAEN MS-CDP",
                "discovery-topic": "homeassistant/sensor"
        },
        "log-level": "WARNING",
        "mqtt": {
                "host": "",
                "pass": "",
                "port": 1883,
                "pub-topic": "home/TheengsGateway/BTtoMQTT",
                "sub-topic": "home/TheengsGateway/+",
                "user": ""
        }
}
```

You need to set at least the MQTT configuration, for instance:

```shell
snap set theengs-gateway mqtt.host=MYBROKER mqtt.user=MYUSER mqtt.pass=MYPASS
```

Have a look at [Theengs Gateway's documentation](https://gateway.theengs.io/use/use.html#details-options) for the meaning of all configuration options.

Then give the snap access to Bluetooth:

```shell
snap connect theengs-gateway:bluez-client :bluez
```

If you're running the snap on Ubuntu Core, this command needs to be:

```shell
snap connect theengs-gateway:bluez-client bluez:service
```

After this, restart the service:

```
snap restart theengs-gateway
```

Theengs Gateway should now run as a service. If you want it to start automatically after booting your Linux distribution, enable the service with:

```shell
snap enable theengs-gateway
```
