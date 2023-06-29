# Broadlink S1C and S2C Alarm Kit Sensors for Home Assistant

__________________________________________

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/custom-components/hacs)
**Name in HACS** : `Broadlink s2c and s1c sensor`</br>
**Component Type** : `platform`</br>
**Platform Name** : `broadlink_s1c`</br>
**Domain Name** : `sensor`</br>

[Community Discussion](https://community.home-assistant.io/t/broadlink-s1c-alarm-kit-custom-sensor-component/45980)</br>

#### Update 2023.06
Update code to work on Home Assistant 2023.6 
code write by rnsalinero taken from [Community Discussion](https://community.home-assistant.io/t/broadlink-s1c-alarm-kit-custom-sensor-component/45980/214)

#### Component Description
Home Assistant Custom Component for integration with [Broadlink S1C Alarm Kit] and [Broadlink S2C Alarm Kit].</br>
S1C And S2C Alarm Kit is a alarm system made by Broadlink, it's made of a Hub which can control up to 16 designated devices:
- Door/Window Sensor
- Motion Detector
- Key Fob

According to Broadlink's site, more sensor types are to released eventually.</br>
The uniqueness of this system is its integration with the rest of the Broadlink smart home products, for instance you can create an interaction as they call it, and make it so the your Broadlink TC2 switch will be turned on when the door sensor is open.</br>
But... If you're in this repository, You probably looking for a way to integrate this system with Home Assistant, so that last fact doesn't really matters.</br>
So, let's get to it! ;-)</br>

**Table Of Contents**
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
  - [Configuration Keys](#configuration-keys)
- [States](#states)
  - [All Sensors](#all-sensors)
  - [Door Sensor](#door-sensor)
  - [Motion Detector](#motion-detector)
  - [Key Fob](#key-fob)
- [Special Notes](#special-notes)

## Requirements
- **Home Assistant
- Your S1C Hub or S2C Hub needs to have a **Static IP Address** reserved by your router.

## Installation
(recomended)

If you have HACS (Home Assistant Community Store) installed at your HA, just search for broadlink_s1c_s2c and install it direct from HACS. HACS will keep track of updates and you can easly upgrade to the latest version when a new release is available.

(manual installation)

- Copy the files https://github.com/nick2525/broadlink_s1c_s2c/tree/master/custom_components/ to your `ha_config_dir/custom_components/` directory.
- Configure like instructed in the Configuration section below.
- Restart Home-Assistant.

## Configuration
To use this component in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml

sensor:
  - platform: broadlink_s1c
    ip_address: xxx.xxx.xxx.xxx
    mac: "xx:xx:xx:xx:xx:xx"
    timeout: 10
```

### Configuration Keys
- **ip_address** (*Required*) Inherited from *homeassistant.const.CONF_IP_ADDRESS*: The IP Address assigned to your device by your router. A static address is preferable.</br>
- **mac** (*Required*) Inherited from *homeassistant.const.CONF_MAC*: The MAC Address of your S1C Hub.</br>
- **timeout** (*Optional*) Inherited from *homeassistant.const.CONF_TIMEOUT*: Timeout value for S1C Hub connectio. *Default=10*.</br>

## States
### All Sensors
- `tampered`
- `unknown` - Inherited from *homeassistant.const.STATE_UNKNOWN*

### Door Sensor
- `open` - Inherited from *homeassistant.const.STATE_OPEN*
- `closed` - Inherited from *homeassistant.const.STATE_CLOSED*

### Motion Detector
- `no_motion`
- `motion_detected`

### Key Fob
- `disarmed` - Inherited from *homeassistant.const.STATE_ALARM_DISARMED*
- `armed_away` - Inherited from *homeassistant.const.STATE_ALARM_ARMED_AWAY*
- `armed_home` - Inherited from *homeassistant.const.STATE_ALARM_ARMED_HOME*
- `sos`

## Special Notes
- Initial configuration of the sensor in the Broadlink App is required.
- The platform discovers the sensors upon loading, therefore if you add another sensor, restart Home Assistant and the new sensors will be added to HA.
- The entity name of each sensor is constructed from the original sensor name from the Broadlink App concatenated with the platform name. Spaces and dashes will be replaced with underscores.</br>
  For instance, if you sensor is name *Bedroom Door* the entity name will be *broadlink_s1c_bedroom_door*, and to reference it you will call *sensor.broadlink_s1c_bedroom_door*
- Although this component is designed for S1C Hubs, it is working well with S2C Hubs too.

