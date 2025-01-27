#MAX-M10S Device Configuration

## Overview
The MAX-M10S GNSS receiver requires configuration to set the desired baud rate and enable the diagnostic messages that we want to use. This particular u-blox device has two layers of storage we can use, RAM and battery backed RAM. There is no flash storage on the MAX-M10S, unfortunately.

RAM settings are volatile and will not persist across power cycles. BBR settings will provide a battery backup of configured RAM settings that are designed to persist across power cycles until the BBR battery is depleted.

According to u-blox documentation for the M10S, fully charged BBR can retain its stored configuration for up to two weeks. In practice, new devices received from the manufacturer do not have any charge in the BBR battery and we have seen them drop settings and revert to default in less than an hour after being plugged into a USB power source for approximately fifteen minutes. We have also observed that when a previously discharged MAX-M10S is reconnected to power within 10 approximately minutes after completion of configuration, it successfully retains settings in BBR.

## Configuration in u-center2
u-center2 is u-blox's proprietary software suite that has the capability to perform serial comms with and configuration of u-blox M10 series devices.  Open u-center2, connect to the MAX-M10S via a serial interface (FTDI or CH340 works great), and click the gear icon (data source configuration). In the new Device Configuration window, under Saved Configurations, click the "+ import" button and import the file `XB1_GPS_Logger_v2.ucf`. Click the Send button to send this configuration to the device. Once the last two messages are sent, the baudrate of the device will be changed from the default of 9600 to the desired rate of 115200 which will kill the connection to ucenter2. Reconnect to the devide (make sure autobaud is enabled) and it should negotiate a new connection at 115200 baud. Re-send the configuration file again and you should see all green checkmarks for every item in the list. 

Once configuration is complete, make sure to connect the MAX-M10S to a power source within 15 minutes (to be safe) to ensure that the configuration is not lost. Note that this does not require connection of the openlog device - just a power source.

## TODO: Configuration over serial via OpenLog firmware
Theoretically the exact same configuration messages can be sent to the MAX-M10S from any serial device and there is no requirement to perform this configuration using u-center2.

This would provide a significant advantage of performing all desired configuration of the MAX-M10S during power-in automatically which would dramatically reduce the complexity of operation and also reduce the likelihood of performing a misconfiguration. Theoretically all condiguration could be done solely in RAM and there would be no requirement for BBR whatsoever.

Care needs to be given to baud rate assumptions and fallback logic. When the MAX10S reverts to factory settings after BBR depletion, it resets to 9600 baud. In ucenter2, if you change the baud from 9600 to 115200, any subsequently issued serial commands will fail until the connection is reestablished at the new baudrate.

## TODO: Investigate possibility of configuring using one-time onboard flash
Similar to configuring over serial during startup (using the openlog as described above), ublox offers provisions in the MAX-M10S to permanently "burn-in" a desired configuration into the device. The MAX-M10S contains fusible memory that offers a one-time write capability but this process cannot be undone. As `gps-diagnostic-logger` is still in early development, it did not make sense to use this capability yet.

This method can be performed in u-center2 and does not require any custom firmware on either device.


