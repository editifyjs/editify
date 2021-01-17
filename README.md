![npm](https://img.shields.io/npm/v/editifyjs)

# editifyjs

Modern, block-style, completely free (MIT license) and pioneering Vue editor!

### Project setup
```
npm install editifyjs
```

### Usage
##### Import editifyjs component and fontawesome-free
```javascript
// main.js

import Vue from "vue"
import App from "./App.vue"
import editifyjs from "editifyjs";
import "@fortawesome/fontawesome-free/css/all.css";

Vue.component(editifyjs)
```
##### Usage in other components
```html
<!-- App.vue -->

<template>
  <div>
    <editifyjs :blocks="blocks" heading="Modern Vue.js editor" />
    
    <!-- 
        * If you want it to be readonly, you should use readonly="true" directly!
    -->
    <editifyjs :blocks="blocks" heading="Modern Vue.js editor" readonly="true" />
  </div>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    blocks: [
      {
        type: "text",
        content: "Modern, block-style, completely free (MIT license) and pioneering Vue editor",
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "blockquote",
        content: "This editor component, which you can use in your vue js projects as you wish, includes many <u>features</u>:",
        theme: "monokai",
        mode: "javascript",
      },
    ],
  }),
};
</script>
```
#### Available Props

| Prop| Default | Type | Description |
| :---: | :---: | :---: | :---:|
| ```blocks``` | [] | array | mandatory |
| ```heading``` | ""| String | mandatory |
| ```readonly``` | false | Boolean | optional|


#### Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

#### License
[MIT](https://choosealicense.com/licenses/mit/)

Copyright (c) 2020-present, Ömer Çelik 