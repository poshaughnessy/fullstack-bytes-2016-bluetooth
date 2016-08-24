title: Bluetooth for Web Developers
output: public/index.html
style: styles.css
controls: false

--

# Web Bluetooth

### How to control a drone from your browser and more 

<p class="my-name">Peter O'Shaughnessy</p>

[@poshaughnessy](https://twitter.com/poshaughnessy)

--

<h2>Samsung Internet</h2>
<p class="no-margin"><img src="images/samsunginternet.png" alt="Samsung Internet" width="45%"></p>
<p class="caption"><a href="http://bit.ly/what-is-samsung-internet">bit.ly.what-is-samsung-internet</a></p>

--

<p class="media-container fill-h">![ByBox](images/bybox-stockonnect.gif)</p>
<p class="caption">[ByBox Stockonnect app developed by pebble {code}](https://www.bybox.com/)</p>

--

<h2>The physical world and the digital world are merging...</h2>

--

<h2>...And your smartphone <br> is at the centre.</h2>

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

<p class="media-container"><img src="images/pokemon-go-smartwatch.png" alt="Pokemon Go Plus watch" width="60%"/></p>
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

<p class="media-container fill-w">![BLE characteristic properties](images/ble-characteristic-props.png)</p>
<p class="caption">Generic ATTribute profile (GATT)</p>

--

## Comms based on Hex

* `0xff === 255`
* `parseInt('ff', 16) === 255`
* [Uint8Array and DataView](http://www.html5rocks.com/en/tutorials/webgl/typed_arrays/) useful for data buffers

--

<p class="media-container fill-w">![BLE comms](images/bybox-comms.png)</p>

--

## JavaScript-friendly options

* Node
* Cordova
* React Native
* Web Bluetooth

--

## Web Bluetooth

<img src="images/ble-logo.png" alt="BLE logo" class="w-300"/>

--

![caniuse.com](images/web-bluetooth-caniuse.png)
<p class="caption">caniuse.com</p>

--

* Chrome for Android (Marshmallow)
* Chrome OS
* Firefox OS
* Opera

![Web Bluetooth flag](images/web-bluetooth-flag.png)

--

## Origin Trial

Chrome Beta

Register at: [bit.ly/WebBluetoothOriginTrial](http://bit.ly/WebBluetoothOriginTrial)

More info: [bit.ly/OriginTrials](https://bit.ly/OriginTrials)

--

## Samsung Internet

<img src="images/samsunginternet.png" alt="Samsung Internet logo" class="w-300"/>

"Watch this space..."

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

<h2>Testing</h2>

--

> “This is a short list of issues you will encounter if you try to use native Android BLE...”

--

<p class="media-container fill-h">![Sweetblue](images/sweetblue.png)</p>
<p class="caption">[bit.ly/sweetblue-android](http://bit.ly/sweetblue-android)</p>

--

<ul>
  <li>Start with a small list of supported devices</li>
  <li>Allow lots of time for device testing</li>
</ul>  

--

<p class="media-container">![CySmart](images/cysmart.png)</p>
<p class="caption">CySmart with CySmart BLE dongle</p>

--

<p class="media-container">![Wireshark](images/adafruit-ble-sniff.jpg)</p>
<p class="caption">Wireshark with Bluefruit BLE sniffer</p>

--

<h2>Demo time</h2>

--

<p class="media-container">![web-bluetooth-parrot-drone](images/web-drone-screenshot.png)</p>
<p class="caption">[bit.ly/web-bluetooth-drone](http://bit.ly/web-bluetooth-drone)</p>

--

<h2>In case of demo fail</h2>
[bit.ly/web-bluetooth-drone-vid](https://youtu.be/gXu3G3cg52k)

--

<h2>Code time</h2>

--

<h2>We can now program the physical world.</h2>

--

<h1>Thanks!</h1>

<p class="my-name">Peter O'Shaughnessy</p>
<p class="twitter">[@poshaughnessy](https://twitter.com/poshaughnessy)</p>

[peteroshaughnessy.com](http://peteroshaughnessy.com)
