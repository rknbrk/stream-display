# stream-display

A tiny Typescript wrapper around Screen Capture API `getDisplayMedia` that sends screen video feed as `ImageData` to your desired callback.

## Installation

### NPM package

```bash
npm install stream-display
```

and then

```javascript
import StreamDisplay from 'stream-display';
```

### In browser without bundlers

You can take the `dist/stream-display.js` file or use a service like [unpkg](https://unpkg.com/stream-display@latest/dist/stream-display.js). Example:

```html
<script src="https://unpkg.com/stream-display@latest/dist/stream-display.js"></script>
<script>
  const stream = new StreamDisplay(...);
</script>
```

## Usage

```javascript
const processImageData = imageData => {...};
const stream = new StreamDisplay(processImageData);

stream.startCapture();
// ...
stream.stopCapture();
```



### Build a new instance of stream-display:

```javascript
new StreamDisplay(callback, options = {})
```

#### Arguments

- `callback: (image: ImageData) => any` - A function that takes one argument — image data from the screen capture feed
- `options` (optional) — a configuration object, currently can have only one option:
  - `scanInterval: number (ms)` — interval between every callback invocation. Default value — `1000 `. NB: when your tab enters background — most browsers will cap the setInterval at `1000ms` maximum. Setting this value lower will not have any effect.

### Start/stop capture

`async startCapture()` — will trigger the screen capture modal and as soon as user accepts — start sending the `ImageData`. On error will return a rejected `Promise` with the error. A list of possible exceptions can be found on [MDN](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia).

`stopCapture()` — ends the capture session.

## Building

The library is build with Typescript and Typescript is included in `devDependencies`. To build the library locally you need just

```bash
npm install
npm run build
```

A fresh build will be waiting for you in the `/dist` folder.