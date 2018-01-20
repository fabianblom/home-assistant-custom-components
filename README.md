# Home-Assistant Custom Components

Some of my custom components for home-assistant. (http://www.home-assistant.io)

Part of a small Proof of Concept, currently I am too lazy to integrate into upstream at the moment.
Still learning to program in python3 and how to make home-assistant components.

## Toon Thermostat climate component

NOTE: This component only works with rooted Toon devices.
Toon's are Thermostats sold by Eneco a Dutch energy company.

More information about preparing for usage with this component can be found here:
[Eneco Toon as Domotica controller](http://www.domoticaforum.eu/viewforum.php?f=87)

This component reads the Thermostat Mode, Current Temperature and it's Setpoint.
You can also control the thermostat Mode and Setpoint. (target temperature)

### Installation

- Copy file `climate/toon.py` to your `ha_config_dir/custom_components/climate` directory.
- Configure with config below.
- Restart Home-Assistant.

## Usage
To use this component in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry

climate:
  - platform: toon
    name: Toon Thermostat
    host: IP_ADDRESS
    port: 10080
    scan_interval: 10
```

Configuration variables:

- **name** (*Optional*): Name of the device. (default = 'Toon Thermostat')
- **host** (*Required*): The hostname or IP address on which the Toon can be reached.
- **port** (*Optional*): Port used by your Toon. (default = 10080)
- **scan_interval** (*Optional*): Number of seconds between polls. (default = 60)

### Screenshot

![alt text](https://raw.githubusercontent.com/cyberjunky/home-assistant-custom-components/master/screenshots/toon.png "Screenshot")

## Toon Smart Meter sensor component

NOTE: This component only works with rooted Toon devices.

It reads Smart Meter data from your Toon, gathered by the meteradapter.

### Installation

- Copy file `sensor/toon_smartmeter.py`s to your `ha_config_dir/custom_components/sensor` directory.
- Configure with config below.
- Restart Home-Assistant.

## Usage
To use this component in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry

sensor:
  - platform: toon_smartmeter
    host: IP_ADDRESS
    port: 10080
    scan_interval: 10
    resources:
      - gasused
      - gasusedcnt
      - elecusageflowpulse
      - elecusagecntpulse
      - elecusageflowlow
      - elecusagecntlow
      - elecusageflowhigh
      - elecusagecnthigh
      - elecprodflowlow
      - elecprodcntlow
      - elecprodflowhigh
      - elecprodcnthigh
      - elecsolar
      - elecsolarcnt
      - heat
```

Configuration variables:

- **host** (*Required*): The hostname or IP address on which the Toon can be reached.
- **port** (*Optional*): Port used by your Toon. (default = 10080)
- **scan_interval** (*Optional*): Number of seconds between polls. (default = 10)
- **resources** (*Required*): This section tells the component which values to display, you can leave out the elecprod values if your don't generate power and the elecusage*pulse types if you use the P1 connection.

![alt text](https://raw.githubusercontent.com/cyberjunky/home-assistant-custom-components/master/screenshots/toon-smartmeter-badges.png "Toon SmartMeter Badges")

If you want them grouped instead of having the separate sensor badges, you can use this in your `groups.yaml`:

```yaml
# Example groups.yaml entry

Smart meter:
  - sensor.toon_gas_used_last_hour
  - sensor.toon_gas_used_cnt
  - sensor.toon_power_use_cnt
  - sensor.toon_power_use
  - sensor.toon_p1_power_prod_low
  - sensor.toon_p1_power_prod_high
  - sensor.toon_p1_power_prod_cnt_low
  - sensor.toon_p1_power_prod_cnt_high
  - sensor.toon_p1_power_use_cnt_pulse
  - sensor.toon_p1_power_use_cnt_low
  - sensor.toon_p1_power_use_cnt_high
  - sensor.toon_p1_power_use_low
  - sensor.toon_p1_power_use_high
  - sensor.toon_p1_power_solar
  - sensor.toon_p1_power_solar_cnt
  - sensor.toon_p1_heat
```

### Screenshots

![alt text](https://raw.githubusercontent.com/cyberjunky/home-assistant-custom-components/master/screenshots/toon-smartmeter.png "Screenshot Toon SmartMeter")
![alt text](https://raw.githubusercontent.com/cyberjunky/home-assistant-custom-components/master/screenshots/toon-smartmeter-graph-gasused.png "Graph Gas Used")
![alt text](https://raw.githubusercontent.com/cyberjunky/home-assistant-custom-components/master/screenshots/toon-smartmeter-graph-poweruselow.png "Graph Power Use Low")
