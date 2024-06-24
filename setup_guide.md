<!-- Add links to top -->

Setup Guide <!-- omit in toc -->
===============================================
<span style="float:right;margin-right:1em;margin-top:-5em"><img src="images/moode-r900-logotype-clear-black-cropped.png"
width="200px"></span>
(C) Tim Curtis 2017  
(C) @azimuth 2024: Novice Section

### Table of Contents <!-- omit in toc -->

- [1. General Information](#1-general-information)
- [2. Quick Help](#2-quick-help)

# 1. General Information

Access the moOde WebUI using a Browser and one of the URL's below. After the WebUI appears in the Browser use the IOS or Android "Save to Home Screen" option to create a moOde App on the home screen. There is no need to download a separate App.
http://moode | http://moode.local | http://IP_ADDRESS

# 2. Quick Help

Instructions for navigating the moOde WebUI, searching the Library, Preference
and Configuration settings, Multiroom audio and other important information is
in "Quick help" which which is located on the "m" menu and at the link below.
https://github.com/moode-player/docs/blob/main/Quickhelp.pdf

# 3. Novice Setup Instructions

These instructions provide a basic step by step tutorial showing how to use the
Raspberry Pi Imager to prepare and write the moOde OS image to an SD card.
<link or in-doc refereence>

# 4. Operating System (OS) Image

For improved security the OS image does not contain a userid, WiFi SSID or
Hotspot password, and Secure Shell (SSH) access is disabled.

1. REQUIRED: The official Raspberry Pi Imager is required to enable SSH,
create a userid and password and optionally set the host name and WiFi SSID
and password. If a host name is not set in the Imager then the default
host name "moode" will be used.

2. REQUIRED: Userid, password and SSH are required otherwise moOde will not
function correctly. When enabling SSH, select "Use password authentication"
which means the password specified for the userid is to be used.

3. REQUIRED: A Hotspot password is required and can be set after first boot
in the Network Configuration screen. This allows moOde to still be accessable
if it cannot connect to Ethernet or any configured WiFi SSID's.

- OS images are listed in the "Media Player OS" category of the Raspberry Pi
Imager, or if they were downloaded directly from moodeaudio.org they can be
selected via the "Use custom" category in the Imager.

- Refer to the links below for more information on operating system security
and how to download and use the Raspberry Pi Imager.
https://www.raspberrypi.com/software/
https://www.raspberrypi.com/news/raspberry-pi-bullseye-update-april-2022/

To access the OS command console use SSH. An easy to use WebSSH terminal is
available in the System Config screen.

# 5. Wifi Hotspot

To access the Hotspot which is moOde's private 2.4 GHz WiFi network refer to the
default settings below.

- SSID          Moode
- Password      As set in Network Config screen
- URL           http://moode.local | http://172.24.1.1

The Hotspot starts automatically when any of the following are true.

- WiFi SSID is set to "Activate Hotspot" in Network Config.
- WiFi SSID is defined in Network Config but no IP address was assigned after
attempting to connect to the configured SSID or any saved SSID's.

# 6. File Sharing

- SMB File Sharing can be turned on in System Config. SMB (Samba) shares named
NAS, Playlists, and SDCard are automatically created. Each USB disk will also
have a Samba share created that is named after its Disk Label.

- NFS File Sharing can be turned on in System Config. Access and options defaults
are provided but can be manually overridden. Each USB disk will have an NFS
export created whose path is /media/disk_label.

# 7. In-Place Software Updates

- Updates to moOde software are made available periodically and can be downloaded
and installed by clicking "CHECK for software update" in System Config.

# 8. Player Setup And Configuration

1. INITIAL SETUP

 a) Insert boot SD card
 b) Insert ethernet cable or alternatively use WiFi SSID defined in Pi Imager
 b) Power on
 c) http://moode | http://moode.local | http://IP_ADDRESS

# 9. Audio Device Setup

 - USB DEVICE
 a) Plug in USB audio device
 a) Menu, Configure, Audio
 c) Set Output device to to the name of the USB audio device

 - I2S DEVICE
 a) Menu, Configure, Audio
 b) Set Named I2S device or DT overlay to the correct device or overlay name
 c) Menu, Power, Restart
 d) Menu, Configure, Audio
 c) Set Output device to to the name of the I2S audio device

# 10. Add Music Files

 - USB STORAGE DEVICES
 a) Insert USB storage device
 b) Menu, Update library
 c) Wait for completion (no spinner)

 - BOOT SDCARD STORAGE
 a) Menu, Update library
 b) Wait for completion (no spinner)

 - NAS DEVICE
 a) Menu, Configure, Library
 b) CREATE Music source
 c) After SAVE, return to Playback or Library
 d) Menu, Update library
 e) Wait for completion (no spinner)

5. VERIFY AUDIO PLAYBACK

 a) http://moode | http://moode.local | http://IP_ADDRESS
 b) Play one of the radio stations
 c) Switch to Library Folder view
 d) Navigate to the SDCARD/Stereo Test
 e) Play the "LR Channel And Phase" track

# 11. Custom Configurations

Customize the player by using any of the following procedures.

1. CONFIGURE FOR WIFI-ONLY CONNECTION

 - Ethernet cable connected
 a) Insert WiFi adapter or use Pi Integrated WiFi
 b) http://moode | http://moode.local | http://IP_ADDRESS
 c) Menu, Configure, Network
 d) Configure a WiFi connection
 e) Menu, Power, Shutdown
 f) Unplug Ethernet cable
 g) Power on

 - Hotspot mode
 a) Join Hotspot SSID, password = Refer to MOODE OS IMAGE section
 b) http://moode.local | http://172.24.1.1
 c) Menu, Configure, Network
 d) Configure a WiFi connection
 e) Menu, Power, Restart

2. SWITCH FROM WIFI-ONLY BACK TO ETHERNET-ONLY

    a) Plug in Ethernet cable
    b) Menu, Configure, Network
    c) RESET network configuration to defaults
    d) Menu, Power, Shutdown
    e) Remove WiFi adapter
    f) Power on

# 12. REST API

If an HTTP command returns data it is in JSON format following REST guidelines.
The base URL is http://moode/command/?cmd=

get_currentsong
Returns contents of the file /var/local/www/currentsong.txt.
Turn on the Metadata file option in Audio Config to generate this file.

get_output_format
ALSA output format or 'Not playing' is returned.

get_volume
Returns the Knob volume.

set_volume
Sets the knob volume to value N, up or down N or mute toggle.
Arguments: N | -up N | -dn N | -mute

get_cdsp_config
Returns the current CamillaDSP config name

set_cdsp_config
Sets CamillaDSP to the specified config name.
Arguments: A config name from the list of available configs including 'Off'.

set_coverview
Turns CoverView screen saver on or off.
Arguments: -on | -off

upd_library
Submits an "Update library" command.

restart_renderer
Restarts the specified renderer.
Arguments: --bluetooth | --airplay | --spotify | --squeezelite | --plexamp | --roonbridge

MPD commands
See MPD protocol for list of commands.
https://mpd.readthedocs.io/en/latest/protocol.html

Deprecated REST API (http) commands. The following commands have been replaced
by the equivalent commands above and at some point will not be supported. It is
recommened to update scripts to use the new commands.

- vol.sh
- coverview.php
- libupd-submit.php
- restart-renderer.php

# 12. SSH COMMANDS

moodeutl
This command can be used for printing logs, status or for manipulating certain
parts of moOde. For a list of options type moodeutl --help

mpc
This command can be used to control MPD. For a list of options type mpc help

vol.sh
This command can be used to get or set MPD volume and update the volume knob.
For a list of options type /var/www/util/vol.sh --help
To run it type /var/www/util/vol.sh <options>

libupd-submit.php
This command submits a "Library update".
To run it type /var/www/util/libupd-submit.php

coverview.php
This command turns the CoverView screen saver on or off.
To run it type /var/www/util/coverview.php -on | -off

restart-renderer.php
This command restarts the specified renderer.
To run it type /var/www/util/restart-renderer.php --renderer
--bluetooth    Restart Bluetooth
--airplay      Restart AirPlay
--spotify      Restart Spotify Connect
--squeezelite  Restart Squeezelite
--plexamp      Restart Plexamp
--roonbridge   Restart RoonBridge
