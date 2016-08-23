title: Bluetooth for Web Developers
author:
  name: Thank you.
  twitter: poshaughnessy
output: public/index.html
style: styles.css
controls: false

--

# How to Control a Drone from your Browser

### And More - with Web Bluetooth

[@poshaughnessy](https://twitter.com/poshaughnessy)

--

<h2 class="vertical-center">The physical world and the digital world are merging...</h2>

--

<h2 class="vertical-center">...And your smartphone <br> is at the centre.</h2>

--

<p class="media-container fill-h">![Anki Overdrive](images/anki-overdrive.gif)</p>
<p class="caption">[Anki Overdrive](https://anki.com)</p>

--

<p class="media-container fill-w fill-h"><iframe src="https://www.youtube.com/embed/-Y77cUI_z30?t=4s" frameborder="0" allowfullscreen></iframe></p>
<p class="caption">[Physical Web lost dog demo](https://youtu.be/-Y77cUI_z30)</p>

--

<p class="media-container fill-w fill-h"><iframe width="560" height="315" src="https://www.youtube.com/embed/b0GDk-53fTo?t=4s" frameborder="0" allowfullscreen></iframe></p>
<p class="caption">[Physical Web restaurant buzzer](https://youtu.be/b0GDk-53fTo)</p>

--

<p class="media-container">![Pokemon Go Plus watch](images/pokemon-go-smartwatch.png)</p>
<p class="caption">[Pokemon Go Plus watch](http://www.pokemongo.com/en-us/pokemon-go-plus/)</p>

--

## Bluetooth Low Energy

![BLE](images/ble-phone.png)

--

<img src="images/ble-logo.png" alt="BLE logo" class="w-200"/>

* Can constantly advertise presence
* Can last years on coin cell batteries
* ~100 kbps throughput (vs 24 Mbps!)

--

<p class="media-container fill-h">![BLE profiles etc.](images/bluetooth-profiles-etc.png)</p>

--

<p class="media-container vertical-center fill-w">![BLE characteristic properties](images/ble-characteristic-props.png)</p>
<p class="caption">Generic ATTribute profile (GATT)</p>

--

## Comms based on Hex

* `0xff === 255`
* `parseInt('ff', 16) === 255`
* [Uint8Array and DataView](http://www.html5rocks.com/en/tutorials/webgl/typed_arrays/) useful for data buffers

--

<h2 class="vertical-center">Here's one I helped make earlier...</h2> 

--

<p class="media-container fill-h">![ByBox](images/bybox-stockonnect.gif)</p>
<p class="caption">[ByBox Stockonnect app developed by pebble {code}](https://www.bybox.com/)</p>

--

<p class="media-container vertical-center fill-w">![BLE comms](images/bybox-comms.png)</p>

--

## JavaScript-friendly options

* Cordova
* React Native
* Web Bluetooth

--

## Cordova

![Cordova](images/cordova-logo.png)

--

## cordova-plugin-ble-central

<p class="media-container">![cordova-plugin-ble-centra](images/cordova-plugin-ble-central.png)</p>

--

<ul class="long-list">
  <li>startScan</li>
  <li>stopScan</li>
  <li>connect</li>
  <li>disconnect</li>
  <li>read</li>
  <li>write</li>
  <li>startNotification</li>
  <li>stopNotification ...</li>
</ul>

--

```javascript
function onDeviceReady() {
 // Scan for Bluetooth devices
 ble.scan([], 5, onDiscoverDevice, onError);
}

function onDiscoverDevice(device) {

 let listItem = document.createElement('li');
 listItem.innerHTML = `<p>${device.name}</p>`;
 listItem.onclick = connect(device.id);

 deviceList.appendChild(listItem);

}
```

--

```javascript
function connect(deviceId) {
 currentDeviceId = deviceId;
 ble.connect(deviceId, onConnect, onError);
}

function onConnect() {
 ble.startNotification(currentDeviceId, 
    BATTERY_SERVICE, BATTERY_CHARACTERISTIC, 
    onBatteryLevelChange, onError);
}

function onBatteryLevelChange(dataBuffer) {
 let bytes = new Uint8Array(dataBuffer);
 batteryState.innerHTML = bytes[0];
}
```

--

## React Native

![React Native](images/react-logo.png)

--

## react-native-ble

<p class="media-container">![react-native-ble](images/react-native-ble.png)</p>

--

## react-native-cordova-plugin

<p class="media-container">![react-native-cordova-plugin](images/react-native-cordova-plugin.png)</p>

--

## Web Bluetooth

<img src="images/ble-logo.png" alt="BLE logo" class="w-300"/>

--

<div class="vertical-center">
    ![caniuse.com](images/web-bluetooth-caniuse.png)
    <p class="caption">caniuse.com</p>
</div>

--

* Chrome for Android (Marshmallow)
* Chrome OS
* Firefox OS
* Opera

![Web Bluetooth flag](images/web-bluetooth-flag.png)

--

## Origin Trial

Register at: [bit.ly/WebBluetoothOriginTrial](http://bit.ly/WebBluetoothOriginTrial)


More info: [bit.ly/OriginTrials](https://bit.ly/OriginTrials)

--

## Samsung Internet

<img src="images/samsunginternet.png" alt="Samsung Internet logo" class="w-300"/>

Watch this space...

--


```javascript
let options = {filters: [{
                 services: ['battery_service'] }] };
                 
navigator.bluetooth.requestDevice(options)
```

--

<p class="media-container">![Bluetooth pairing screen](images/bluetooth-device-chooser.png)</p>

--

```javascript
  ...
  
  .then(device => device.connectGATT())  
  .then(server =>
    server.getPrimaryService('battery_service'))
  .then(service =>
    service.getCharacteristic('battery_level'))
  .then(characteristic => {
    // Read battery level
    return characteristic.readValue();
  })
  .then(value => {
    let bytes = new Uint8Array(value.buffer);
    console.log(`Battery level: ${bytes[0]}`);
  });
```

<div class="caption">[bit.ly/chrome-bluetooth-guide](http://bit.ly/chrome-bluetooth-guide)</div>

--

<h2 class="vertical-center">Testing</h2>

--

> “This is a short list of issues you will encounter if you try to use native Android BLE...”

--

<p class="media-container fill-h">![Sweetblue](images/sweetblue.png)</p>
<p class="caption">[bit.ly/sweetblue-android](http://bit.ly/sweetblue-android)</p>

--

<div class="vertical-center">
  <ul>
      <li>Start with a small list of supported devices</li>
      <li>Allow lots of time for device testing</li>
  </ul>
</div>  

--

<p class="media-container">![CySmart](images/cysmart.png)</p>
<p class="caption">CySmart with CySmart BLE dongle</p>

--

<p class="media-container">![Wireshark](images/adafruit-ble-sniff.jpg)</p>
<p class="caption">Wireshark with Bluefruit BLE sniffer</p>

--

<h2 class="vertical-center">Demo time</h2>

--

<p class="media-container">![web-bluetooth-parrot-drone](images/web-drone-screenshot.png)</p>
<p class="caption">[bit.ly/web-bluetooth-drone](http://bit.ly/web-bluetooth-drone)</p>

--

<div class="vertical-center">
    <h2>In case of demo fail</h2>
    [bit.ly/web-bluetooth-drone-video](https://youtu.be/-FO9thLaiug)
</div>

--

<h2 class="vertical-center">Code time</h2>
