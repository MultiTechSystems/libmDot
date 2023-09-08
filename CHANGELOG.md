
# Release 4.2.1

Update to library 4.2.1 built with mbed-os-6.16.0
Same version used in AT Firmware v4.2.1

* Updates to pass LCTT 3.10.0_R2
  * Needed to disable auto increment DR to pass MAC_104_BV_019_B and MAC_104_BV_021
  * Needed to select unused channels before reusing channels
* Sleep will save session automatically and restore session after wakeup
* Added getDisableIncrementDR and setDisableIncrementDR to control automatic DR increases if MAC commands and payload to send is larger    than the current DR supports, check bytes available before send with getNextTxMaxSize
* Added custom device-id and serial number to EEPROM, setCustomDeviceID and setCustomSerialNumber
* Added channel selection algorithm to select unused channels before reusing recent channels


# Release 4.1.4

Update to library 4.1.4 built with mbed-os-6.8.0
Same version used in AT Firmware v4.1.5

* Add wake pin trigger
* Add write OTP for mDot only
* Add dutyCycle managment functions for AS923 plans
* Add GLOBAL Channel Plan option
* Update Join Backoff to work over sleep and increase randomness of back-off durations

Fixed: RTC sleep duration above 4294 seconds is now supported


# Release 4.1.0

* Update ChannelPlan_AU915.cpp - add max payload values for DR8-DR13
* Fixed issue where accessing files and sleeping in different threads would cause the MDot to lock up.
* Ability to save a backup of protected settings (Device ID, Network ID, Network Key, and Gen App Key) in MDot One-Time-Programmable storage.
* FOTA session now checks file system for space required to complete file download and upgrade process.  If inadequate space is available files are removed.
* Ability to set trigger for WAKE pin as rising, falling, or either.
* Updated to MBed OS 6.8.
* Support for AS923-4.


# Release 4.0.0

* LoRaWAN 1.0.4
* Regional Parameters 1.0.3rA
* FUOTA - Fragmentation and Multicast Setup v1.0.0
* Support for EU868, US915, KR920, IN865, RU864, AU915, AS923-1, AS923-2, AS923-3 and AS923-JAPAN
* Updated to MBed OS 6.1.

* Configuration Updates
** Changes to the configuration are not backwards compatible with previous versions
** A device will lose all configuration and identification if reverted to a previous firmware
** Configuration is saved with redundancy and wear leveling to increase resiliency and allow recovery after write errors due to loss of power or reset during a write cycle

* mDot sleep can be interrupted by LowPowerTimer expiration when RTC_ALARM_OR_INTERRUPT is used.

* xDot now supports FUOTA when an external SPI flash is provided
** Block Device Requirements
*** For a block device to work with the XDot it must meet the following criteria:
**** Work with MBed OS DataFlashBlockDevice or SPIFBlockDevice classes
**** Maximum 4KB sector erase size
**** Maximum 512 byte page size
**** SPIF type components must support Serial Flash Discoverable Parameters (SFDP)


# Release 3.2.5

## Bug Fixes
* Restore channel mask in AU/US with AT+FSB=0
* Wait for non-zero RSSI during LBT channel activity test
* ADR back-off to DR0
* ADR back-off calculate min-DR from enabled channels


# Release 3.2.1

## Changes
* Upgrade mbed-os to 5.11.1
* Added support for LoRaWAN 1.0.3rA
* Removed AutoSleep functionality
* Added Class B
  * Added BeaconRx and BeaconLost events: mDotEvent.h
  * Added BeaconLocked and BeaconData properties to mDotEvent
  * Added getGPSTime to perform DeviceTimeReq
  * Added ServerTimeSeconds and ServerTimeMillis to mDotEvent to return DeviceTimeAns
  * setDeviceClass accepts argument of "B" to enter beacon acquisition state
  * setPingPeriodicity, getPingPeriodicity to control Class B windows
* getNextTxMaxSize returns available payload bytes for next transmission
* Added getFrequencyOffset, setFrequencyOffset for fine tuning of Tx due to crystal variance

## Bug Fixes
* Invalid MAC commands being processed
  * Verify length of last command
* Lock-up if sleep is called during/before Rx Windows
  * State is reset on wake-up
* Join when class C enabled could report false negative response for Rx2
  * Join timeout extended passed end of Rx2 window in Class C mode
* Repeated calls to restoreNetworkSession will flip channel mask in AU915 and US915
  * Channel mask is restored correctly with multiple calls

## Regressions in 3.2.0
* Downlink 16-bit counter rollover was not handled correctly


# Release 3.2.0

## Changes

* Added support for 1.0.3rA
* Added Class B
* Removed AutoSleep functionality
* Added Class B
  * Added BeaconRx and BeaconLost events: mDotEvent.h
  * Added BeaconLocked and BeaconData properties to mDotEvent
  * Added getGPSTime to perform DeviceTimeReq
  * Added ServerTimeSeconds and ServerTimeMillis to mDotEvent to return DeviceTimeAns
  * setDeviceClass accepts argument of "B" to enter beacon acquisition state
  * setPingPeriodicity, getPingPeriodicity to control Class B windows
* getNextTxMaxSize returns available payload bytes for next transmission
* Added getFrequencyOffset, setFrequencyOffset for fine tuning of Tx due to crystal variance


## Bug Fixes
* Invalid MAC commands being processed
  * Verify length of last command
* Lock-up if sleep is called during/before Rx Windows
  * State is reset on wake-up
* Join when class C enabled could report false negative response for Rx2
  * Join timeout extended passed end of Rx2 window in Class C mode
* Repeated calls to restoreNetworkSession will flip channel mask in AU915 and US915
  * Channel mask is restored correctly with multiple calls
