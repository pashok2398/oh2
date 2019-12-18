## Install Tuya API
`ssh openhab@openhab`

`cd /etc/openhab2/scripts`

`git clone https://github.com/tsightler/tuya-mqtt.git`

`cd tuya-mqtt`

`npm install`

`cp config.json.sample config.json`

`DEBUG=* tuya-mqtt.js`

## Get Tuya device IP
Search in your router / arp -a (by MAC from Smart Life app)

## Get Tuya device key
https://github.com/codetheweb/tuyapi/blob/master/docs/SETUP.md

## Install MQTT
Addons -> Bindings -> MQTT Binding -> `install`

Addons -> Misc-> MQTT Broker -> `install`

Inbox -> + -> MQTT Binding -> ADD MANUALLY -> MQTT Broker **set** `Broker Hostname/IP` to `127.0.0.1`

Inbox -> + -> MQTT Binding -> ADD MANUALLY -> Generic MQTT Thing -> Bridge Selection -> MQTT Broker

Configuration -> Things -> Generic MQTT Thing -> Channels -> + -> :

`MQTT State Topic = tuya/ver3.3/<Tuya ID>/<Tuya KEY>/<Tuya IP>/state`

`MQTT Command Topic = tuya/ver3.3/<Tuya ID>/<Tuya KEY>/<Tuya IP>/state`

`Custom On/Open Value = 0`

`Custom Off/Closed Value = 1`

Configuration -> Things -> Generic MQTT Thing -> Channels -> <Channel Name> -> Linked items -> + -> 
`Please select a profile: Default`

`Please select the item to link: +Create New Item...`

`Name = <AnyName> #You will need it for sitemap`

`Type = Switch`

`LINK`

Control -> `Check the button`

## Add to Mobile App

`ssh openhab@openhab`

`cd /etc/openhab2/sitemaps`

`vi <AnyName>.sitemap`

```
sitemap boiler label="My home automation" {
    Frame label="Demo" {
        Switch item=<TheNameOfTheItem> # The name of the item from the link step
        }
    }
```

`sudo systemctl restart openhab2.service`
