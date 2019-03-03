---
layout: page
title: otb-iot
permalink: /otb-iot-old/
---

<html lang="en-us">
  <head>
    <meta charset="UTF-8">
    <title>otb-iot by piersfinlayson</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" type="text/css" href="stylesheets/normalize.css" media="screen">
    <link href='https://fonts.googleapis.com/css?family=Open+Sans:400,700' rel='stylesheet' type='text/css'>
    <link rel="stylesheet" type="text/css" href="stylesheets/stylesheet.css" media="screen">
    <link rel="stylesheet" type="text/css" href="stylesheets/github-light.css" media="screen">
  </head>
  <body>
    <section class="page-header">
      <h1 class="project-name">otb-iot</h1>
      <h2 class="project-tagline">Out of The Box Internet Of Things</h2>
      <a href="https://github.com/piersfinlayson/otb-iot" class="btn">View on GitHub</a>
      <a href="https://github.com/piersfinlayson/otb-iot/zipball/master" class="btn">Download .zip</a>
      <a href="https://github.com/piersfinlayson/otb-iot/tarball/master" class="btn">Download .tar.gz</a>
    </section>

    <section class="main-content">
      <hr>

<h1>
<a id="out-of-the-box---internet-of-things" class="anchor" href="#out-of-the-box---internet-of-things" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Out of the Box - Internet of Things</h1>

<h2>
<a id="introduction" class="anchor" href="#introduction" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Introduction</h2>

<p><a href="https://piersfinlayson.github.io/otb-iot/">otb-iot</a> is software for ESP8266 devices which is intended to make the ESP8266 quick and easy to deploy for <em>real</em> applications, and to be <em>robust</em>.</p>

<p>There's a huge amount of hacking and playing going on with the ESP8266 today, which is a fantastic thing for all hobbyists, enthusiasts and those looking to develop deployable products.  But while it's very quick and easy to get stuff running on the ESP8266, and even to cobble together something that provides a lot of function, making it fully featured enough to actually deploy and maintain in the field takes effort.</p>

<p>This is where otb-iot comes in - it's a complete software image for the ESP8266 which is intended to be this robust and deployable solution.</p>

<h2>
<a id="getting-started" class="anchor" href="#getting-started" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Getting Started</h2>

<p>I've tried to make it as easy as possible to get started.  There are five main steps:</p>

<ul>
<li>Install the <a href="https://github.com/pfalcon/esp-open-sdk">open-esp-sdk</a>
</li>
<li>(Optional) Install <a href="http://platformio.org/#!/get-started">platformio</a>
</li>
<li>Clone the otb-iot software from <a href="https://github.com/piersfinlayson/otb-iot">github</a>
</li>
<li>Build it</li>
<li>Install it</li>
</ul>

<p>I strongly recommend using linux as the build environment.  If like me you won't touch a linux desktop environment with a barge-pole you may want to run linux as a virtual machine within a hypervisor such as <a href="https://www.virtualbox.org/">VirtualBox</a>, and then ssh into it from your Windows or Mac.</p>

<h3>
<a id="open-esp-sdk" class="anchor" href="#open-esp-sdk" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>open-esp-sdk</h3>

<p>The simple instructions to install this are <a href="https://github.com/pfalcon/esp-open-sdk#requirements-and-dependencies">here</a>.  It takes me about an hour from scratch to install this piece - as I have pretty slow internet access.</p>

<h3>
<a id="platformio" class="anchor" href="#platformio" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>platformio</h3>

<p>This is only used by the otb-iot Makefile to provide a convenient serial monitor.  Doubtless there's easier ways to get this function - but I started out using the ESP8266 Arduino framework and platformio is awesome at making this easy.  Follow the CLI instructions <a href="http://platformio.org/#!/get-started">here</a>.</p>

<h3>
<a id="otb-iot" class="anchor" href="#otb-iot" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>otb-iot</h3>

<h4>
<a id="getting-the-software" class="anchor" href="#getting-the-software" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Getting the software</h4>

<pre><code>git clone https://github.com/piersfinlayson/otb-iot.git
</code></pre>

<h4>
<a id="building-it" class="anchor" href="#building-it" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Building it</h4>

<ul>
<li>
Go to the directory you've cloned otb-iot</p>

<pre><code>cd otb-iot</code></pre>
</li>
<li>
<p>Ensure you expose SDK_BASE from your shell, pointing at the base open-esp-sdk directory - or uncomment this line in the Makefile and make sure it's set correctly:</p>

<pre><code># SDK_BASE = /opt/esp-open-sdk</code></pre>
</li>
<li>
<p>Check ESP_SDK is set correctly in the Makefile to point to the Espressif SDK within the open-esp-sdk directory:</p>

<pre><code>ESP_SDK = esp_iot_sdk_v1.4.0</code></pre>
</li>
<li>
<p>Run configure to check out submodules</p>

<pre><code>./configure</code></pre>
</li>
<li>
<p>Run make</p>

<pre><code>make</code></pre>
</li>
</ul>

<h4>
<a id="installing-it" class="anchor" href="#installing-it" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Installing it</h4>

<ul>
<li><p>Plug your ESP8266 to a USB port on your machine - either using the port provided by a dev board like Nodemcu or the WeMos D1-mini, or using a separate FTDI/CH340/etc serial to USB converter.  If you're using linux in a VM you'll need to set up a rule within your hypervisor to route the USB device to the VM.  Note only boards with 4MB (32Mbit) of flash (or greater) are currently supported.  This seems to be all of the current batch of ESP-12s coming out of China at the moment.</p></li>
<li>
<p>Use make to flash your device:</p>

<pre><code></code>make flash_initial</code></pre>
</li>
</ul>

<p>That's it - you should now be up and running</p>

<h4>
<a id="using-otb-iot" class="anchor" href="#using-otb-iot" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Using otb-iot</h4>

<p>There's more detailed information later, but in a nutshell to start using otb-iot:</p>

<ul>
<li>Connect to the "OTB-IOT.XXXXXX" WiFi Access Point which will now be available.</li>
<li>This should activate captive portal on your device, but if not point a browser at <a href="http://192.168.4.1">http://192.168.4.1</a>
</li>
<li>Configure

<ul>
<li>Your WiFi credentials (access point SSID and password)</li>
<li>Your MQTT server details (IP address and any username/password)</li>
</ul>
</li>
<li>Hit submit</li>
</ul>

<p>The ESP8266 will now reboot and should connect to your WiFi network.  The WiFi AP will be exposed at all times to allow you to reconfigure the above details while MQTT isn't connected.  When MQTT is connected by default the AP will turn off, but you can override this behaviour both within the captive portal, and using MQTT if you desire.</p>

<p>You can now start communicating with your ESP8266 over MQTT.  To check it's responding send to topic <em>/otb_iot/all/system</em> message <em>ping</em>.  You should get a message <em>pong</em> sent to topic <em>/otb_iot/all/status</em>. </p>

<p>To use mosquitto to send and receive MQTT messages run this command in one shell:</p>

<pre><code>mosquitto_sub -v -h _your_mqtt_server_ -t /#
</code></pre>

<p>to listen for all MQTT publishes.</p>

<p>And then in another:</p>

<pre><code>mosquitto_pub -h _your_mqtt_server_ -t /otb_iot/all/system -m ping
</code></pre>

<p>to send the ping.  You should see a message like this in response:</p>

<pre><code>/otb_iot/xxxxxx/status pong
</code></pre>

<p>where xxxxxx is the chip ID of your ESP8266.</p>

<h2>
<a id="iot-function" class="anchor" href="#iot-function" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>IOT Function</h2>

<p>Today otb-iot provides the following IOT functionality:</p>

<ul>
<li><p>Support for reporting temperatures from <a href="http://www.hobbytronics.co.uk/ds18b20-arduino">DS18B20</a> sensors over MQTT</p></li>
<li><p>Ability to set GPIO output to high and low over MQTT</p></li>
<li>
<p>Access to various management capabity over MQTT including</p>

<ul>
<li>Over the Air (OTA) upgrades</li>
<li>Reconfiguration</li>
<li>Querying wifi signal strength</li>
<li>Querying GPIO status</li>
<li>Reset/reboot</li>
<li>Retrieving logs and last reboot reason</li>
</ul>
</li>
</ul>

<h2>
<a id="supported-boards" class="anchor" href="#supported-boards" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Supported boards</h2>

<p>Anything with at least 4MB (32MBit) of flash should be supported.  It would probably be possible to squeeze down to 2MB fairly easily, but I've not seen any 2MB boards out there.  As otb-iot includes 3 boot images for robustness, squeezing into 1MB would be problematic.</p>

<p>This means that any recent (early 2016) ESP-12 should work.  Most of my testing has been done with:</p>

<ul>
<li><p><a href="http://www.wemos.cc/wiki/doku.php?id=en:start">WeMos D1-mini</a> (my favourite)</p></li>
<li><p><a href="https://cknodemcu.wordpress.com/2015/11/13/nodemcu-variants/">Nodemcu V3 from LoLin</a> (a bit big)</p></li>
</ul>

<p>To see check your board size run:</p>

<pre><code>esptool.py flash_id
</code></pre>

<p>If you get 4016 reported you're good to go.</p>

<h2>
<a id="mqtt-api" class="anchor" href="#mqtt-api" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>MQTT "API"</h2>

<p>I took the decision to use <a href="http://mqtt.org/">MQTT</a> as the primary communication protocol because</p>

<ul>
<li>it's suited to IOT applications due to its lightweight nature (both requiring little footprint for implementation, and having little protocol overhead on messages)</li>
<li>to keep functionality limited - remember a focus here is to be robust and stable, which is hard with a plethora of function.</li>
</ul>

<p>Therefore only very limited configuration is available over HTTP.</p>

<h3>
<a id="sending-and-receiving-messages" class="anchor" href="#sending-and-receiving-messages" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Sending and Receiving Messages</h3>

<p>To send messages to the otb-iot device, use one of the following topics:</p>

<pre><code>/otb_iot/all/system - Addresses all otb-iot devices attached to your MQTT broker
/otb_iot/chipid/system - To just address your device
/otb_iot/loc1/loc2/loc3/chipid/system - To just address your device, if you've set the loc1, loc2 and loc3 values
</code></pre>

<p>Regular status updates and responses to messages sent on the system topic will be sent using one of the following topics:</p>

<pre><code>/otb_iot/chipid/status - if loc1, loc2 and loc3 aren't set
/otb_iot/loc1/loc2/loc3/chipid/status - if they are set
</code></pre>

<p>The otb-iot device may also send using one of the following topics when reporting serious errors:</p>

<pre><code>/otb_iot/chipid/error
/otb_iot/loc1/loc2/loc3/chipid/error
</code></pre>

<p>Temperature readings will be sent once a minute for each attached DS18B20 using:</p>

<pre><code>/otb_iot/loc1/loc2/loc3/chipid/temp/sensor_loc/sensorid
</code></pre>

<p>Loc1, loc2 and loc3 will be included only if configured, as will sensor_loc.  All temperature readings are in Celsius, and the DS18B20 claims +-0.5C accuracy.</p>

<h3>
<a id="system-messages" class="anchor" href="#system-messages" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>System Messages</h3>

<p>The support messages are as follows:</p>

<p>To set config values:</p>

<pre><code>config:set:field:value
</code></pre>

<p>Field may be one of:</p>

<pre><code>ssid      # WiFi SSID
password  # WiFi Password
loc1      # Location 1 to use in topics
loc2      # Location 2 to use in topics
loc3      # Location 3 to use in topics
keep_ap_active  # Keep AP active when MQTT connected
</code></pre>

<p>To set DS18B20 sensor_loc information:</p>

<pre><code>config:set:ds18b20:addr:loc  # To set a location
config:set:ds18b20:clear     # To clear all DS18B20 location information
</code></pre>

<p>The address format for DS18B20 sensors is 28-112233445566 (not including checksum)</p>

<p>To retrieve config values:</p>

<pre><code>config:get:field     # Values as above
config:get:ds18b20s  # To get the number of _configured_ DS18B20s (i.e. locations)
config:get:ds18b20:addr   # To get DS18B20 info by address
config:get:ds18b20:loc    # To get DS18B20 info by location
config:get:ds18b20:slot   # To get DS18B20 by slot - up to 8 (0-7) are supported 
</code></pre>

<p>To get info about actual connected DS18B20s (as opposed to configured address/locations):</p>

<pre><code>ds18b20:get_num          # Gets number of devices connected at last book
ds18b20:get:ds18b20:num  # Where num starts at 0 and goes up to 7 depending on number of connected - returns address in above format
</code></pre>

<p>To retrieve received signal strength of connected AP:</p>

<pre><code>rssi:get
</code></pre>

<p>To get current free heap size of ESP8266:</p>

<pre><code>heap_size:get
</code></pre>

<p>To reset (reboot) the device use either:</p>

<pre><code>reset
reboot
</code></pre>

<p>To ping the device over MQTT:</p>

<pre><code>ping
</code></pre>

<p>To retrieve last reboot reason:</p>

<pre><code>reason:reboot
</code></pre>

<p>To get otb-iot software version;</p>

<pre><code>version:get
</code></pre>

<p>To get ESP8266 chip ID:</p>

<pre><code>chip_id:get
</code></pre>

<p>To get software compile date:</p>

<pre><code>compile_date:get
</code></pre>

<p>To get software compile time:</p>

<pre><code>compile_time:get
</code></pre>

<p>To see which boot slot the software is currently running from:</p>

<pre><code>boot_slot:get
</code></pre>

<p>To set the slot to boot from at next reset:</p>

<pre><code>boot_slot:set:value  # 0 or 1
</code></pre>

<p>To set GPIO value:</p>

<pre><code>gpio:set:pin_no:value  # value = 0 or 1, pin=2 is reserved for DS18B20s
</code></pre>

<p>To apply and save GPIO value so it's applied after next reset (NOT YET IMPLEMENTED):</p>

<pre><code>gpio:save:pin_no:value
</code></pre>

<p>To get current pin value:</p>

<pre><code>gpio:get:pin_no
</code></pre>

<p>To update to new software, which installs in the non-current boot slot and reboots when done:    </p>

<pre><code>update:ip_address:port:path    # Uses HTTP for update
upgrade:ip_address:port:path   # Uses HTTP for update
</code></pre>

<p>To retrieve logs from RAM:</p>

<pre><code>logs:ram:get:num   # 0 = most recent, 1 is next, 2 is next, etc
</code></pre>

<p>To retreive logs from flash where they are stored in the event of a serious problem leading to reboot.  (While storing of logs in this case is supported, retrieving over MQTT is NOT YET IMPLEMENTED):    </p>

<pre><code>logs:flash:get:num  (0 = most recent, 1 is next, …)
</code></pre>

<h3>
<a id="status-messages" class="anchor" href="#status-messages" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Status Messages</h3>

<p>otb-iot will send responses to system messages using status messages.  It may also send unsolicited messages in some cases - like when rebooting after an upgrade.</p>

<p>The messages that may be sent are as follows:</p>

<pre><code>config:set:ok(:further_info)
config:set:error(:further_info)
config:get:ok:value(:further_info)
config:get:error(:further_info)
gpio:set:ok(:further_info)
gpio:set:error(:further_info)
gpio:get:ok:value
gpio:get:error(:further_info)
boot_slot:set:ok(:further_info)
boot_slot:set:error(:further_info)
boot_slot:get:ok:value
boot_slot:get:error(:further_info)
heap_size:get:ok:value
heap_size:get:error(:further_info)
pong(:further_info)
error(:further_info)
reset:ok(:further_info)
reboot:ok(:further_info)
reset:error(:further_info)
reboot:error(:further_info)
update:ok(:further_info)
update:error(:further_info)
booted unsolicited
version:version_id
build_date:build_date
build_time:build_time
chipid:chipid 
reason:further_info
offline unsolicited (MQTT Last Will and Testament generated by the MQTTbroker)
</code></pre>

<h3>
<a id="error-messages" class="anchor" href="#error-messages" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Error Messages</h3>

<p>In the case of a serious error hit by otb-iot it will attempt to send on the error topic a message containing error details</p>

<h3>
<a id="message-format" class="anchor" href="#message-format" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Message format</h3>

<p>As can be seen colon (:) is used to separate fields and parameters in otb-iot MQTT messages.  Colons are not therefore support in values themselves.</p>

<p>In addition whitespace will not be used - any whitespace characters will be converted to _ before being sent in status or error messages.</p>

<h2>
<a id="logging" class="anchor" href="#logging" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Logging</h2>

<p>otb-iot outputs useful logs over serial.  It also has a circular log buffer in RAM which can be queried via MQTT.  In the event of a serious error leading to a reset forced by the otb-iot software this will be written to flash.  In the future this flash region will be queryable via MQTT.</p>

<p>otb-iot logs fall into the following categories:</p>

<ul>
<li>ERROR</li>
<li>WARN</li>
<li>INFO</li>
<li>DEBUG (compiled out by default)</li>
</ul>

<h2>
<a id="robustness" class="anchor" href="#robustness" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Robustness</h2>

<p>A number of approaches are taken to ensuring otb-iot's robustness:</p>

<ul>
<li><p>Starting the WiFi AP if MQTT fails, so WiFi and MQTT details can easily be reconfigured as necessary.</p></li>
<li><p>Hardening of the various function provided, handling error codes, and taking corrective recovery on errors.</p></li>
<li><p>Ongoing checking of internal consistency.</p></li>
<li><p>Substantial logging via serial and access to this over MQTT.</p></li>
<li><p>Ability to query device in an automated fashion over MQTT using provided APIs.</p></li>
<li><p>Limiting the exposed function.</p></li>
<li><p>Checksuming of software images, and fallback to alternative image.</p></li>
<li><p>"Factory" Installed 3rd software recovery image, not upgradeable via OTA to allow recovery.</p></li>
</ul>

<p>This is still a work in progress.</p>

<h2>
<a id="security" class="anchor" href="#security" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Security</h2>

<p>This is a work in progress.  Currently MQTT implementation does not support SSL.  WiFi AP passwords are not logged and are not queryable via APIs.</p>

<h2>
<a id="third-party-component-usage" class="anchor" href="#third-party-component-usage" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Third Party Component Usage</h2>

<ul>
<li><p><a href="https://github.com/pfalcon/esp-open-sdk">pfalcon's Open ESP SDK</a></p></li>
<li><p><a href="http://bbs.espressif.com/viewtopic.php?f=46&amp;t=850">Espressif ESP non-RTOS SDK</a></p></li>
<li><p><a href="https://github.com/tuanpmt/esp_mqtt">tuanpmt's MQTT</a></p></li>
<li><p><a href="https://github.com/raburton/rboot">raburton's rboot</a> and <a href="https://github.com/raburton/esptool2">Esptool2</a></p></li>
<li><p><a href="https://github.com/Spritetm/esphttpd">Spritetm's esphttpd</a></p></li>
<li><p><a href="http://www.pjrc.com/teensy/td_libs_OneWire.html">Paul Stroffgen's One Wire library</a></p></li>
<li><p><a href="https://github.com/nekromant/esp8266-frankenstein">Necromant's adaption of the One Wire library in esp8266-frankenstein</a></p></li>
</ul>

<h2>
<a id="otb-iot-license" class="anchor" href="#otb-iot-license" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>otb-iot License</h2>

<p>The otb-iot software is licensed under the <a href="http://www.gnu.org/licenses/">GNU General Public License version 3 (GPLv3)</a>.</p>

<p>All of the original versions of the third party code are licensed under their respective licenses, with any new code licensed under the GPLv3.</p>

      <footer class="site-footer">
        <span class="site-footer-owner"><a href="https://github.com/piersfinlayson/otb-iot">otb-iot</a> is maintained by <a href="https://github.com/piersfinlayson">piersfinlayson</a>.</span>
      </footer>

    </section>

  
  </body>
</html>