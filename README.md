# hassio-modbus2mqtt

Image

## Add-ons

This repository contains the following add-ons

### [modbus2MQTT add-on](./modbus2mqtt)

![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]


## Installation
1. If you don't have an MQTT broker yet; in Home Assistant go to **[Settings → Add-ons → Add-on store](https://my.home-assistant.io/redirect/supervisor_store/)** and install the **[Mosquitto broker](https://my.home-assistant.io/redirect/supervisor_addon/?addon=core_mosquitto)** addon.
1. Go back to the **Add-on store**, click **⋮ → Repositories**, fill in</br>  `https://github.com/modbus2mqtt/hassio-modbus2mqtt` and click **Add → Close** or click the **Add repository** button below, click **Add → Close** (You might need to enter the **internal IP address** of your Home Assistant instance first).  
[![Open your Home Assistant instance and show the add add-on repository dialog with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fmodbus2mqtt%2Fhassio-modbus2mqtt)
3. The repository includes two add-ons:
    - **modbus2MQTT** is the stable release that tracks the released versions of modbus2MQTT. (**recommended for most users**)
    - **modbus2MQTT Edge** tracks the `dev` branch of modbus2MQTT such that you can install the edge version if there are features or fixes in the modbus2MQTT dev branch that are not yet released.
4. Click on the addon and press **Install** and wait till the addon is installed.
5. Click on **Configuration**
    - If you are **not** using the Mosquitto broker addon, Configure the MQTT brocker connection data in the modbus2mqtt Configuration menu 
    - If you don't know the port and you have just one USB device connected to your machine try `/dev/ttyUSB0`. Else use the [Home Assistant CLI](https://www.home-assistant.io/common-tasks/os#home-assistant-via-the-command-line) and execute `ha hardware info` to find out. 
    - Click **Save**
    - **Tip:** it is possible to refer to variables in the Home Assistant `secrets.yaml` file (not the modbus2MQTT one!) by using e.g. `password: '!secret mqtt_pass'`
1. Start the addon by going to **Info** and click **Start**
1. Wait till modbus2MQTT starts and press **OPEN WEB UI** to verify modbus2MQTT started correctly.
    - If it shows `502: Bad Gateway` wait a bit more and refresh the page.
    - If this takes too long (e.g. 2 minutes +) check the **Log** tab to see what went wrong.

For more information see [the documentation](https://github.com/modbus2mqtt/hassio-modbus2mqtt/blob/master/modbus2mqtt/DOCS.md).

## Restoring data from a standalone installation

1. Ensure that both environments are running the same version
1. Backup your standalone environment `data` folder (possibly leaving out the `logs/` folder)
1. Configure your serial port using the HA addon configuration UI
1. Restore your `data` folder contents into `/usr/share/hassio/homeassistant/modbus2mqtt`
1. Edit the `/usr/share/hassio/homeassistant/modbus2mqtt/configuration.yaml` file:
    - Ensure that the serial port section matches the one configured with the UI
    - Remove any irrelevant sections from the config (e.g. `mqtt`, `advanced/log_syslog`, `frontend`)
1. Start the add-on

## Changelog
The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/).

All notable changes to this project will be documented in the [CHANGELOG.md](modbus2mqtt/CHANGELOG.md) file.

Version for releases is based on [modbus2MQTT](https://github.com/modbus2mqtt/modbus2mqtt) format: `X.Y.Z`.

Any changes on the addon that do not require a new version of modbus2MQTT will use the format: `X.Y.Z-A` where `X.Y.Z` is fixed on the modbus2MQTT release version and `A` is related to the addon.

Edge version will not maintain a CHANGELOG and doesn't have a version.

## Issues
If you find any issues with the add-on, please check the [issue tracker](https://github.com/modbus2mqtt/hassio-modbus2mqtt/issues) for similar issues before creating one. If your issue is regarding specific devices or, more generally, an issue that arises after modbus2MQTT has successfully started, it should likely be reported in the [modbus2MQTT issue tracker](https://github.com/Koenkk/modbus2mqtt/issues).

Feel free to create a PR for fixes and enhancements. 

### Testing changes locally

If you're submitting a PR and wish to test it locally:
- Gain root access to your Home Assistant installation
- In the Add-on Settings, Ensure "Watchdog" is turned off so the container isn't automatically restarted when it's stopped via the CLI

- Enter the `modbus2mqtt` container interactively.
```sh
docker exec -it $(docker ps | grep modbus2mqtt | cut -d" " -f 1) /bin/sh
```
- Edit the file you'd like to test & save. 
```sh
vi server/src/mqttdiscover.ts
```
- Back on the Home Assistant installation, restart the `modbus2mqtt` container
```sh
docker restart $(docker ps | grep modbus2mqtt | cut -d" " -f 1)
```
- Refresh the web UI and perform your testing.

## Credits
- [danielwelch](https://github.com/danielwelch)
- [ciotlosm](https://github.com/ciotlosm)
- [Koenkk](https://github.com/Koenkk)
- [volkmarnissen](https://github.com/volkmarnissen)

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg