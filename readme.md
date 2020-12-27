# 💡 philips hue sdk

<a href="https://www.npmjs.com/package/@bradgarropy/hue-sdk">
    <img alt="npm" src="https://img.shields.io/npm/v/@bradgarropy/hue-sdk.svg?style=flat-square">
</a>

<a href="https://www.npmjs.com/package/@bradgarropy/hue-sdk">
    <img alt="npm" src="https://img.shields.io/npm/dt/@bradgarropy/hue-sdk?style=flat-square">
</a>

_[Philips Hue][hue] SDK for managing smart devices._

## 📦 Installation

This package is hosted on [npm][npm].

```bash
npm install @bradgarropy/hue-sdk
```

## 🚦 Setup

In order to use the Philips Hue API you must have a [Philips Hue Bridge][bridge] installed. You need the ip address and a user account to send commands to the bridge.

Locate the ip address by navigating to https://discovery.meethue.com in a web browser. This should respond with an array of all discovered bridges on your wifi network, typically there will only be one. You'll see the ip address in the `json` object which we will call the `HUE_BRIDGE_IP`.

```json
[
    {
        "id": "001728fdfe70920f",
        "internalipaddress": "192.168.84.129"
    }
]
```

Then navigate to `https://<BRIDGE_IP_ADDRESS>/debug/clip.html`. Use the API Debugger to create a new user as follows.

```
url:    /api
method: POST
body:   {"devicetype": "<USERNAME>"}
```

You should receive a response with the message `"link button not pressed"`.

Now go press the large button on top of your [Philips Hue Bridge][bridge], then send the same command again. You should get back a success message with a `username` property, this will be the `HUE_USERNAME`.

_You can find more information on the Philips Hue Developer [Get Started][get-started] page._

## 🥑 Usage

Now that all of the setup is done, here's how to send your first command to the bridge. Use the `HUE_BRIDGE_IP` and the `HUE_USERNAME` from the [Setup](#-setup) section above to initialize a `Hue` client.

```javascript
const Hue = require("@bradgarropy/hue-sdk")

const hue = new Hue(process.env.HUE_BRIDGE_IP, process.env.HUE_USERNAME)
const lights = await hue.readLights()

console.log(lights)
```

## 📖 API Reference

### `readLight(id)`

Get all information for a single light.

| Name | Example  | Description |
| ---- | -------- | ----------- |
| `id` | `abc123` | Light id.   |

```javascript
hue.readLight("abc123")
```

### `readLights()`

Get all information for all lights.

```javascript
hue.readLights()
```

### `updateLight(id, state)`

Update a light's state.

| Name    | Example       | Description  |
| ------- | ------------- | ------------ |
| `id`    | `abc123`      | Light id.    |
| `state` | `{on: false}` | Light state. |

```javascript
hue.updateLight("abc123", {on: false})
```

### `turnOnLight(id)`

Turn on a specific light.

| Name | Example  | Description |
| ---- | -------- | ----------- |
| `id` | `abc123` | Light id.   |

```javascript
hue.turnOnLight("abc123")
```

### `turnOffLight(id)`

Turn off a specific light.

| Name | Example | Description |
| ---- | ------- | ----------- |
| `id` |         | Light id.   |

```javascript
hue.turnOffLight("abc123")
```

### `setBrightness(id, brightness)`

Set the brightness of a specific light.

| Name         | Example  | Description               |
| ------------ | -------- | ------------------------- |
| `id`         | `abc123` | Light id.                 |
| `brightness` | `128`    | Brightness level (1-254). |

```javascript
hue.setBrightness("abc123", 128)
```

### `setColor(id, color)`

Set the color of a specific light.

| Name    | Example  | Description                                                                              |
| ------- | -------- | ---------------------------------------------------------------------------------------- |
| `id`    | `abc123` | Light id.                                                                                |
| `color` | `blue`   | Light color. (random, white, red, orange, yellow, green, blue, purple, lime, teal, pink) |

```javascript
hue.setColor("abc123", "blue")
```

### `setRandomColor(id)`

Set a specific light to a random color.

| Name | Example  | Description |
| ---- | -------- | ----------- |
| `id` | `abc123` | Light id.   |

```javascript
hue.setRandomColor("abc123")
```

## ❔ Questions

🐛 report bugs by filing [issues][issues]  
📢 provide feedback with [issues][issues] or on [twitter][twitter]  
🙋🏼‍♂️ use my [ama][ama] or [twitter][twitter] to ask any other questions

[get-started]: https://developers.meethue.com/develop/get-started-2
[bridge]: https://www.philips-hue.com/en-us/p/hue-bridge/046677458478
[hue]: https://developers.meethue.com
[npm]: https://www.npmjs.com/package/@bradgarropy/hue-sdk
[issues]: https://github.com/bradgarropy/hue-sdk/issues
[twitter]: https://twitter.com/bradgarropy
[ama]: https://bradgarropy.com/ama
