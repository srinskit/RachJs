# RachJs: A Javascipt client for Rach
## Install and use
From CDN
```
https://cdn.jsdelivr.net/gh/srinskit/RachJs@master/index.js
```
## Usage
Browser
```
<!DOCTYPE html>
<html>

<head>
    <title>Rach test</title>
</head>

<script type="module">
    // Import latest ES6 module
    import Rach from 'https://cdn.jsdelivr.net/gh/srinskit/RachJs@master/index.js';
    const rach = new Rach('ws://localhost:8080/', { username: 'su', password: 'pass' });
    rach.enable_debug();
    var one_two_pub;
    function on_rach_start() {
        // Register publisher
        one_two_pub = rach.add_pub("/one/two");
    }
    window.pub_on_click = function () {
        // Publish data
        if (one_two_pub)
            one_two_pub.pub(Date());
    }
    // Start Rach on window load
    window.onload = () => rach.start(on_rach_start);
    // Stop Rach before window unload
    window.onbeforeunload = () => rach.stop();
</script>

<body>
    <button onclick="pub_on_click()">PUB</button>
</body>

</html>
```
