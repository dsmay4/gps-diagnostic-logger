
# gps-diagnostic-logger
A lightweight, standalone Global Positioning System (GPS)/Global Navigation Satellite System (GNSS) data capture and logging device to troubleshoot signal quality and interference issues.

## Background
gps-diagnostic-logger was developed for the Boom Supersonic XB-1 program to assist in characterizing and quantifying radio frequency (RF) interference that adversely impacted performance of the aircraft's onboard GPS devices. The test program called for a small, self-contained piece of diagnostic equipment that could be carried onboard an experimental aircraft to collect data without requiring integration into the aircraft itself.

## Features
* u-blox MAX-M10S GNSS receiver 
* u-blox active Multi-band Active GNSS Antenna (L1/L5)
* Sparkfun OpenLog microSD serial data logger
* 9V battery/power supply
* Records and logs the following GPS/GNSS data:
	* Position/Time/Velocity data for the following constellations:
		* GPS/SBAS (L1C/A)
		* Galileo (E1C)
		* Beidou (BII D1)
		* Glonass
	* Space Vehicle (SV) information including carrier-to-noise ratio
	* RF Spectral data (freqency vs power) around L1 (1574.42 MHz)
	* u-blox proprietary interference-related diagnostic data fields
* Data is recorded to microSD card and can be viewed in PyGPSclient or parsed with pyubx2
