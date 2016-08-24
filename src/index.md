title: Bluetooth for Web Developers
output: public/index.html
style: styles.css
controls: false

--

# Web Bluetooth

### How to control a drone from your browser and more 

<div class="group-closer">
  <p>Peter O'Shaughnessy</p>
  <p>[@poshaughnessy](https://twitter.com/poshaughnessy)</p>
</div>

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

<h2>...And your smartphone is at the centre.</h2>

--

<p class="media-container fill-h">![Anki Overdrive](images/anki-overdrive.gif)</p>
<p class="caption">[Anki Overdrive](https://anki.com)</p>

--

<p class="media-container"><img src="images/pokemon-go-smartwatch.png" alt="Pokemon Go Plus watch" width="60%"/></p>
<p class="caption">[Pokemon Go Plus watch](http://www.pokemongo.com/en-us/pokemon-go-plus/)</p>

--

<p class="media-container">![Bluetooth friends](images/bluetooth-friends.jpg)</p>

--

## Bluetooth Low Energy

![BLE](images/ble-phone.png)

--

<img src="images/ble-logo.png" alt="BLE logo" class="w-200"/>

* Can constantly advertise presence
* Can last years on coin cell batteries
* ~100 kbps throughput (vs 24 Mbps!)

--

<h2>Generic ATTribute profile (GATT)</h2>
<p class="media-container"><img src="images/bluetooth-profiles-etc.png" alt="GATT" width="40%"/></p>

--

<p class="media-container"><img src="images/ble-characteristic-props.png" alt="BLE characteristic properties" width="75%"/></p>

--

## Hex in JavaScript

* `0xff === 255`
* `parseInt('ff', 16) === 255`
* ArrayBuffer, Uint8Array and DataView

[bit.ly/html5-rocks-typed-arrays-guide](http://www.html5rocks.com/en/tutorials/webgl/typed_arrays/)

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

Chrome Beta or Chrome Dev (Chrome stable soon)

Register at: [bit.ly/WebBluetoothOriginTrial](http://bit.ly/WebBluetoothOriginTrial)

More info: [bit.ly/OriginTrials](https://bit.ly/OriginTrials)

--

## Samsung Internet

<img src="images/samsunginternet.png" alt="Samsung Internet logo" class="w-300"/>

*Watch this space...*

--

```javascript
navigator.bluetooth.requestDevice({
  filters: [{
    name: 'SomeAmazingRobot'
  }],
  optionalServices: ['battery_service']
})
...
```

--

<p class="media-container fill-h"><img src="images/bluetooth-pairing-prompt.png" alt="Bluetooth pairing prompt"/></p>

--

```javascript
  ...
  
  .then(device => device.connectGATT())  
  .then(server => server.getPrimaryService('batt_service'))
  .then(service => service.getCharacteristic('batt_level'))
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

<h2>Physical Web</h2>

<p class="media-container"><img src="images/physical-web-logo.png" alt="Physical Web logo" width="30%"/></p>

A discovery service for 'smart' objects

--

<p class="media-container">![Physical Web bus example](images/physical-web-bus.png)</p>
<p class="caption">["London buses test out the Physical Web"](http://marketingland.com/london-buses-test-first-consumer-experience-physical-web-170529)</p>

--

<p class="media-container fill-w fill-h"><iframe width="560" height="315" src="https://www.youtube.com/embed/b0GDk-53fTo?t=4s" frameborder="0" allowfullscreen></iframe></p>
<p class="caption">[Physical Web restaurant buzzer](https://youtu.be/b0GDk-53fTo)</p>

--

<p class="media-container fill-h"><img src="images/physical-web-enable.png" alt="Enabling Physical Web"/>

--

<h2>Eddystone-URL</h2>
<p class="media-container"><img src="images/eddystone-format.png" alt="Eddystone URL format" width="65%"/></p>

--

<h2>Bluetooth Testing</h2>

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

<p class="media-container fill-h">![CySmart](images/cysmart.png)</p>
<p class="caption">[CySmart with CySmart BLE dongle (Windows)](http://www.cypress.com/documentation/software-and-drivers/cysmart-bluetooth-le-test-and-debug-tool)</p>

--

<p class="media-container">![CySmart app](images/bluetooth-debugging-apps.png)</p>
<p class="caption">Bluetooth debugging apps: LightBlue, Bluefruit, CySmart</p>

--

<p class="media-container fill-h">![Wireshark](images/adafruit-ble-sniff.jpg)</p>
<p class="caption">[Wireshark](https://www.wireshark.org/) with [Bluefruit BLE sniffer](https://shop.pimoroni.com/products/adafruit-bluefruit-le-sniffer-ble-4-0-nrf51822-v1-0)</p>

--

<h2>Demo time</h2>
<p class="no-margin"><img src="images/web-drone-screenshot.png" width="30%" alt="Web Drone Controller"/></p>
<p class="caption">[bit.ly/web-bluetooth-drone](http://bit.ly/web-bluetooth-drone)</p>

--

<h2>In case of demo fail</h2>
[bit.ly/web-bluetooth-drone-vid](https://youtu.be/gXu3G3cg52k)

--

<h2>Code time</h2>

--

<h2>The physical world is now at your command.</h2>

--

<h1>Thanks!</h1>

<div class="group-closer">
  <p>Peter O'Shaughnessy</p>
  <p>[@poshaughnessy](https://twitter.com/poshaughnessy)</p>
  <p>[peteroshaughnessy.com](http://peteroshaughnessy.com)</p>
</div>

<div class="group-closer">
  <p>Samsung Internet Developer Relations</p>
  <p>[@sbrowserdevrel](https://twitter.com/sbrowserdevrel)</p>
  <p>[medium.com/samsung-internet-dev](https://medium.com/samsung-internet-dev)</p>
</div>
