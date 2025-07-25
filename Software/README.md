# **PD Stepper** - More Software Info

#### If you just received your PD Stepper see the [Setup Instructions](https://github.com/joshr120/PD-Stepper/tree/main/Getting%20Started) for how to get started

## Arduino Upload settings: ##
When uploading software with the Arduino IDE ensure you have first installed the ESP32 Add-on in Arduino IDE there are [many tutorials](https://randomnerdtutorials.com/installing-esp32-arduino-ide-2-0/) on how to do this.

The Board type should be set as "ESP32S3 Dev Module"

USB CDC on Boot should be set to "Enabled"

![upload settings](https://github.com/joshr120/PD-Stepper/assets/120012174/f002548a-ec56-4bae-93c7-10ec5e83b6d1)


## ESPHome: ##
>If you have not used ESPHome before follow the offical [getting started guide](https://esphome.io/guides/getting_started_hassio.html). Select ESP32-S3 as the board type. The custom .yaml can then be copied from the repo into the configuration editor. Ensure you also add you WiFi SSID and password to your "Secrets".

The **PD-Stepper-Blinds-Advanced.yaml** config file uses the [custom TMC2209](https://github.com/slimcdk/esphome-custom-components/tree/master/esphome/components/tmc2209) component by [slimcdk](https://github.com/slimcdk). It also uses the AS5600 encoder so that if the blinds are manually moved it will not lose its end positions. Thanks to the custom componenet the example can also be modified to use stall gaurd for sensorless homing. PD voltage can be configured and it set an startup. 
> By default this will use the power on position as the OPEN position.

> If the motor spins but the cover stays in the "open" position it means either your encoder is not working or your motor is spinning in the opposite direction releative to your encoder. You can swap which lambda function is commented out to reverse the encoder direction. 

> You can enable sensorless homeing (Stallguard) by uncommenting line 129, you may need to tune the threshold and current values to get this to work well.

The **PD-Stepper-Blinds-Simple.yaml** config file simply treats the TMC2209 as a a4988 driver. The microsteps and PD voltage are set at startup by GPIO pins and the motor is driven via the STEP and DIR pins.

The **PD-Stepper-Position-Control.yaml** config also uses the [custom TMC2209](https://github.com/slimcdk/esphome-custom-components/tree/master/esphome/components/tmc2209) component by @slimcdk. It is a more stripped down version of PD-Stepper-Blinds-Advanced.yaml allowing you to set the position of the motor using a simple slider. A good base for use cases other than blinds.

These examples also present the buttons, LEDs, power good and bus voltages to the ESPHome interface so you can do what you like with them.

