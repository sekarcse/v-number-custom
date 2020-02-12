# vue-number-custom

`Works with Vue 2.*`

## Installation

```sh
$ npm install vue-number-custom --save
```

### Install as Component
```js
import Vue from 'vue'
  
export default {
  name: 'App',

  components: {
    VueNumber
  }
}
```

### Install as Plugin
```js
import Vue from 'vue'
import VueNumberCustom from 'vue-number-custom'
  
Vue.use(VueNumberCustom)
```

## Usage

### Quick example

```vue
<template>
  <vue-number-custom v-model="price"></vue-number-custom>
</template>

<script>
import VueNumberCustom from 'vue-number-custom'

export default {

  name: 'App',

  components: {
    VueNumberCustom
  },

  data: () => ({
    price: 100
  }),
}
</script>

```

## License

vue-number is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)