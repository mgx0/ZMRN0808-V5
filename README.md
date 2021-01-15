# ZMRN0808-V5 ETH relay board
information about "smart" 8ch relay board.

- Ethernet chip is 83848KSQ with transformer
- CPU is NXP LPC1768FBD100


MQTT topics (SN stands for serial number:

v5+SN+ctr
v5+SN+state

v5249cbb189f4b9cctr
v5249cbb189f4b9cstate


set relay state:
0 - off
1 - on
2 - toggle
x - no change



mosquitto_pub -h 10.0.0.1 -d -t v5xxxxxxxxxxxxxxctr -m '{"cmd":"post","output":"11111111"}' 
mosquitto_pub -h 10.0.0.1 -d -t v5xxxxxxxxxxxxxxctr -m '{"cmd":"post","output":"2x2x2x2x"}'  // 2 goes for pulse





state.cgi
relay.cgi?pulse1=pulse
relay.cgi?relayoff1=off
relay.cgi?relayon1=on
System.cgi
relay.cgi
rs485.cgi
zm.cgi     // mosquitto configuration. do not change serial number, this will revert back after reboot. Topic is without / prefix
settings.cgi
network.cgi
scene.cgi
time.cgi - some chinese page dependent on MS XML, do not use for your mental health's sake