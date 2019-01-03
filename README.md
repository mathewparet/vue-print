# @mathewparet/vue-print

> A way to quickly print portion of a website.

## Install

``` bash
npm install @mathewparet/vue-print
```

## Load Globally
```js
import Print from '@mathewparet/vue-print';
Vue.use(Print);
```

## Install in current scope
```js
import Print from '@mathewparet/vue-print';
export default {
    components: {
        Print
    }
}
```

## Usage
```html
<print ref="printData">
    <h1>Hello World</h1>
    <p class="print-hidden">I am hidden during print</p>
</print>
```

## Methods
### ```print()```

Call this method to initiate print.

```js
this.$refs.printData.print();
```

## Attributes

Name | Required | Type | Default | Description
--- | --- | --- | --- | ---
```auto-close``` | No | Boolean | ```true``` | If ```true``` the print popup window will close when the print dialogue closes
```use-manifest``` | No | Boolean | ```true``` | If ```true``` the ```/mix-manifest.json``` file is called to identify the latest ```print-css``` file. If no manifest is found, it falls back to use the ```print-css``` file without version
```print-css``` | No | String | ```'/css/print.css'``` | Defnes the default print.css file.

## Classes

### ```print-hidden```

Use this class for elements that shouldn't be printed.

## Events

### ```print-closed```

This event is fired when print window is closed.