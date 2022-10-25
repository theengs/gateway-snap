[![Build status](https://github.com/theengs/gateway-snap/workflows/Build/badge.svg)](https://github.com/theengs/gateway-snap/actions)
[![Check status](https://github.com/theengs/gateway-snap/workflows/Check/badge.svg)](https://github.com/theengs/gateway-snap/actions)
[![GitHub license](https://img.shields.io/github/license/theengs/gateway-snap.svg)](https://github.com/theengs/gateway-snap/blob/development/LICENSE)
[![theengs-gateway](https://snapcraft.io/theengs-gateway/badge.svg)](https://snapcraft.io/theengs-gateway)

# Theengs Gateway Snap

[Theengs Gateway](https://github.com/theengs/gateway) packaged as a snap.

## How to install

[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-white.svg)](https://snapcraft.io/theengs-gateway)

You can install the snap on amd64, arm64 and armhf systems with:

```shell
snap install theengs-gateway
```

If you're running this on Ubuntu Core on a Raspberry Pi, also install the following snaps for Bluetooth:

```shell
snap install bluez pi-bluetooth
```

## How to configure

First give the snap access to Bluetooth:

```shell
snap connect theengs-gateway:bluez-client :bluez
```

If you're running the snap on Ubuntu Core, this command needs to be:

```shell
snap connect theengs-gateway:bluez-client bluez:service
```

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
                "discovery-topic": "homeassistant/sensor",
                "hass-discovery": 1
        },
        "log-level": "WARNING",
        "mqtt": {
                "host": "",
                "pass": "",
                "port": 1883,
                "pub-topic": "home/TheengsGateway/BTtoMQTT",
                "sub-topic": "home/+/BTtoMQTT/undecoded",
                "user": ""
        }
}
```

You need to set at least the MQTT configuration, for instance:

```shell
snap set theengs-gateway mqtt.host=MYBROKER mqtt.user=MYUSER mqtt.pass=MYPASS
```

Have a look at [Theengs Gateway's documentation](https://gateway.theengs.io/use/use.html#details-options) for the meaning of all configuration options.

After changing the configuration, Theengs Gateway should now run as a service. If you want it to start automatically after booting your Linux distribution, enable the service with:

```shell
snap start --enable theengs-gateway
```
