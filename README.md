# ESPHome code for LilyGo Higrow boards

This is first but also working version of ESPHome code to get HiGrow board from LilyGo working.

For now only version with DHT sensor are supported but I plan to add support for BME version also.

# Setup

Copy YAML file of your choice (for now only `higrow_dht.yaml` is tested and working) into your ESPHom folder.
Change file name to match your future plant name.

You now have option to use MQTT instead of or parallel with API Home Assistant integration.

# Configuration

Minimum reqiured configuration is to adapt/change subsctitution section in YAML file:

```
substitutions:
  devicename: "schefflera_arboricola"
  upper_devicename: Schefflera Arboricola
  awake_duration: 6s      
  sleep_duration: 90min   
  update_interval: 5s
  fixed_ip: 192.168.2.50
```

* `devicename` should be lowercas name of the plant. If you use `-` instead of `_`, you will probably receive error when installing or validating code.
* `upper_devicename` is used to create user friendly name in Home Assistant
* `awake_duration` is time that board will stay awake. Due to WiFi connection problems, don't lower this. Even at 5 seconds it can decrease chance for successful connection
* `sleep_duration` is period how long will board sleep to preserve battery usage
* `update_interval` is period when board should make sure it updates sensor data and sends to HA. Needs to be less than awake time
* `fixed_ip` is used to define FIXED IP address of the board. DHCP can add extra lag for connection.
* `gateway_ip` is you network gateway IP address
* `subnet_mask` is subnet mask used in your network

## Secrets

Don't forget to add to secrets file:
```
wifi_ssid: YOUR_WIFI_SSID
wifi_password: "YOUT_WIFI_PASSWORD"
```

Also, if you plan to use MQTT, uncomment MQTT section in YAML file:
```
#mqtt:
#  broker: mqtt_ip
#  username: mqtt_user
#  password: mqtt_password
```
If you are not useing MQTT authentication with username and password, you can leave them commented out.
And in secrets file from ESPHome add following 3 lines:
```
# MQTT
mqtt_ip: 192.168.1.XXX
mqtt_user: MQTT_USER
mqtt_password: MQTT_PASSWORD
```

## Calibration

Calibration is not necessary, but will definitly improve your experience.

I use glass of water to calibrate maximum soil humidity (minimum is just dry it off).

And next optiona calibration is battery maximum V.

## Issues

I'm still playing with battery % as it's not reading it correctly. It always stays at 100%, but I think I've managed to pinpoint on possible issues.
