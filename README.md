
HomeKit proxy allows you to controll HomeKit enabled Devices from HomeBridge. This is especially usefull if you want to allow Android/Linux or Windows users to access HomeKit-Exclusive devices. This is an almost complete rewrite of the original homebridge-homekit-controller by MartinPham. 

The Plugin currently supports the following Services provided by **WLAN**-based HomeKit enabled devices:
 - `Switch`
 - `Outlet`
 - `Motion Sensors`
 - `Temperatur Sensors`
 - `Humidity Sensors`
 - `CO2 Sensors`
-  `Carbon Monoxid Sensors`
 - `Air Quality Sensors`
 - `Ambient Light Sensors`
 - `Light Bulbs`
 - `Battery/Charging State`

BLE is currently not supported, as it seems to be unstable when multiple BLE-enabled Plugins are installed.

All supported sensors on any configured device are automatically dicovered and added when HomeBridge starts up.
# Install
```
sudo npm i -g homebridge-homekit-proxy
```

or if you'd like to run the beta versions, you can use
```
sudo npm install -g homebridge-homekit-proxy@beta
```

# Pair devices

## Discover Devices
```
homekit [network interface]
```

### Example

```
homekit
```

or

```
homekit wlan0
```

- Select device, and enter code to pair (including `-`, example `123-45-678`)
- Enter filename to save pairing's informations JSON
- Inside the JSON file, you can find

```
{
    "id": "device id",
    "name": "device name",
    "address": "device ip",
    "port": device-port,
    "pairingData": {
        "AccessoryPairingID": "xxx",
        "AccessoryLTPK": "xxx",
        "iOSDevicePairingID": "xxx",
        "iOSDeviceLTSK": "xxx",
        "iOSDeviceLTPK": "xxx"
    },
    "accessories": {
        "accessories": [...]
    }
}
```
- Note down the `"id"`, `"name"`, `"address"`, `"port"` and `"pairingData"`
  



## Config
This Plugin supports the Configuration Interface in Homebridge UI (homebridge-config-ui-x). Simply add a new Device and paste the values you obtained above.

Here are some additional configuration parameters, not obtained by the Device Pairing:
- `services.historyInterval` (*boolean*): **true** will enable fakeGato for compatible Sensors. This will allow you to view a history in the EVE-App
- `services.historyInterval` (optional, *numeric*): Determins the Interval used to take readings. The valus range is **[30, 600]**. The default value is **600**
- `services.uniquePrefix`(optional, *string*): When a device is added to multiple HomeBridge instances in the same network, you will need to provide a unique prefix. Otherwise Eve-App will get confused.

### Example
```
{
    "platforms": [
        {
            "platform": "HomeKitProxy",            
            "services": [
                {
                    "id": "device id",
                    "name": "device name",
                    "address": "device ip",
                    "port": "device port",
                    "historyInterval": 0
                    "pairingData": {
                        "AccessoryPairingID": "xxx",
                        "AccessoryLTPK": "xxx",
                        "iOSDevicePairingID": "xxx",
                        "iOSDeviceLTSK": "xxx",
                        "iOSDeviceLTPK": "xxx"
                    }
                }
            ]
        }    
    ]
}
```

# Building
The project was converted to the build system from https://github.com/homebridge/homebridge-plugin-template. Visual Studio Code is set up to lint on save. 

Using `npm run dev` will launch the develop environment, where your code is automatically compiled on save and the local homebridge server is automatically restarted.

The command `npm rund build` will trigger the compilation of your project manually.

# Tested Accesories

- Quingping Air Monitor Lite (Cleargrass Luftdetektor Lite, Cleargrass Air Monitor Lite)

Please let me know if you use this plugin and got it to work with a new HomeKit-Accesory that is not listed above