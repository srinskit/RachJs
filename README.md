# RachJs: A Javascipt client for Rach

[![NPM](https://nodei.co/npm/rachjs.png)](https://nodei.co/npm/rachjs/)

## Install and use
From CDN
```
https://cdn.jsdelivr.net/gh/srinskit/RachJs@master/index.js
```
From NPM
```
npm install rachjs
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
ReactJs
```
import React, {Component} from "react";
import Rach from "rachjs";

class App extends Component {
    constructor(props) {
        super(props);
        this.state = {
            connectedToRach: false,
        };
        this.rach = new Rach("ws://localhost:8080", {username: "test", password: "pass"});
        this.rach.enable_debug();
    }

    componentDidMount() {
        this.rach.start(() => {
            this.setState({connectedToRach: true});
        });
    }

    componentWillUnmount() {
        this.rach.stop();
    }

    render() {
        return (<div>"Hi"</div>);
    }

}

export default App;
```