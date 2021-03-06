# 05_Connecting
The fourth project will focus on connecting to the Internet using the [built-in Wifi module](https://github.com/tessel/t1-docs/blob/master/wifi.md#connect-tessel-to-wifi).

Before we use the Wifi module, set up a local `creds` module with your Wifi network credentials.

## Instructions
Going through the creds workflow once more. There are more efficient ways to manage your secrets, but this is an effective and relatively easy solution for local development with the Tessel & public source code management like Github.

- Add `**/creds` to your .gitignore
- With `04_Connecting` as your current working directory:
```
mkdir creds
cd creds
touch index.js
```
Paste the below script into `index.js` and enter values
```node
// Creds.js
// Enter values for your network
var network = '#####'
var netpass = '#####'
var sec = 'wpa2' // other options are 'wep', 'wpa', or 'unsecured'

var creds = {};

var wifiSettings = { ssid: network,
                     password: netpass,
                     security: sec,
                     timeout: 30
                   };


creds.wifiConfig = wifiSettings;

module.exports = creds;
```

### Usage
Example usage of `creds` modules

```node
var wifi = require('wifi-cc3000')
var creds = require("./creds") // reference to local module

// provide `wifiConfig` object to `wifi` hardware module
wifi.connect(creds.wifiConfig)
```

See the sketches in this folder for real use cases.

## Wifi Connection issues
Below are Tessel's troubleshooting instructions. For further debugging, see Tessel V1 [Wifi documentation](https://github.com/tessel/t1-docs/blob/master/wifi.md#connecting-to-wifi-from-js).


Check to see if Tessel is connected to wifi using Tessel CLI, `tessel wifi -l`.
If there is no IP address, the Tessel is not connected to Wifi.
Try power cycling your Tessel and then run the tessel wifi connection command again.
- Remove saved wifi profiles => `tessel stop; tessel wifi -d`
- Move closer to the router.
- Reset the router.
- Make sure the router has b/g mode enabled and isn't using channels 12, 13, or 14.


### Dependencies
- [delay-ms](https://github.com/thelostspore/delay-ms)
- [q](https://github.com/kriskowal/q)
