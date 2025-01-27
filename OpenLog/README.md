
# Sparkfun OpenLog Configuration

## microSD setup
Ensure the microSD card is formated as FAT32 and is 32GB or smaller in size.

## config.txt
The file `config.txt` goes into the root directory of the microSD card used in the SparkFun openlog device. It contains the configuration for the device and is compatible with OpenLog firmware V4.3. The only change to the `config.txt` file in this repo is to increase the baud rate from default 9600 to 115200.

## OpenLog Firmware
`gps-diagnostic-logger` was tested successfully with OpenLog firmware v4.2 and v4.3 in both OpenLog and OpenLog_Light variants. OpenLog_Light is preferred since we have no need to use the serial terminal interface to interact with the openlog device and OpenLog_Light has a larger buffer to minimize the likelihood of dropped messages.

Follow the instructions in the https://learn.sparkfun.com/tutorials/openlog-hookup-guide to load OpenLog_Light v4.3 onto the openlog device.

