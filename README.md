# ZMRN0808-V5 ETH relay board
information about "smart" 8ch relay board. This is what I have collected from the vendor, firmware file and eeprom content. Give or take, this was a bloody nightmare to get.

I have bought two of these boards from Aliexpress, got two sealed boards, that's it. They even had two different firmware versions. Seller did not have a clue when I asked for ANY KIND OF INFORMATION. Manual, description, addresses .. nothing. Vendor is iotzone.cn and they have provided me documents in attached folder. I wish everyone not to deal with such a stupid seller like I did.

- Ethernet chip is 83848KSQ with transformer
- CPU is NXP LPC1768FBD100


## relay mask

set relay state (applies to MQTT, TCP and GET requests. Probably RS485 too but I did not bother to test):
0 - off
1 - on
2 - toggle
x - no change


## MQTT
these are mosquitto commands to turn a relay on/off/pulse. Do not forget to set MQTT broker to your own, otherwise your board connects to Chinese MQTT as per firmware's default

mosquitto_pub -h 10.0.0.1 -d -t v5xxxxxxxxxxxxxxctr -m '{"cmd":"post","output":"11111111"}' 
mosquitto_pub -h 10.0.0.1 -d -t v5xxxxxxxxxxxxxxctr -m '{"cmd":"post","output":"2x2x2x2x"}'  // 2 goes for pulse

the board is subscribed to the topic and listens for commands: v5+SN+ctr
and it publishes status in some interval at this topic: v5+SN+state

for example:
v5249caa44955c1cctr
v5249cbb44955c1cstate

Note: there is no slash as prefix so you won't be able to see the board messages by subscribing to "/#"

## Digital IO pins
I did get the digital inputs working. I think reading the manual (which I did not have at the time of writing) should be enough to do it.

## Flashing
flash the board by putting INT pin LOW and connecting power. Then use Flash Magic (Windows only, I'm afraid) to send the hex file in attached folder

## URLs
These are probably all possible webpages to go to, once logged into the web interface
- state.cgi
- relay.cgi?pulse1=pulse
- relay.cgi?relayoff1=off
- relay.cgi?relayon1=on
- System.cgi
- relay.cgi
- rs485.cgi
- zm.cgi     // mosquitto configuration. do not change serial number, this will revert back after reboot. Topic is without / prefix
- settings.cgi
- network.cgi
- scene.cgi
- time.cgi - some chinese page dependent on MS XML, do not use for your mental health's sake
