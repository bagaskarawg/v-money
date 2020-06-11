# v-money Mask for Vue.js

## Features

- Lightweight (<2KB gzipped)
- Dependency free
- Mobile support
- Component or Directive flavors
- Accept copy/paste
- Editable
- Built-in `money` filter (https://github.com/vuejs-tips/v-money/pull/30)
- Min / Max Limits (https://github.com/vuejs-tips/v-money/pull/36)

## Usage

### A. Globally

Register component and directive globally:

```js
import Vue from 'vue'
import money from 'v-money'

// register directive v-money and component <money>
Vue.use(money, {precision: 4})
```

Register only directive globally:

```js
import Vue from 'vue'
import { VMoney } from 'v-money'
// register only directive v-money
Vue.directive('money', VMoney)
```

### B. Use as component: https://jsfiddle.net/auom8st8/

```html
<template>
  <div>
    <money v-model="price" v-bind="money"></money> {{ price | money }}
  </div>
</template>

<script>
  import {Money} from 'v-money'

  export default {
    components: {Money},

    data () {
      return {
        price: 123.45,
        money: {
          decimal: ',',
          thousands: '.',
          prefix: 'R$ ',
          suffix: ' #',
          precision: 2,
          masked: false, /* doesn't work with directive */
          min: 0,
          max: 1000
        }
      }
    }
  }
</script>
```

### C. Use as directive: https://jsfiddle.net/nj3cLoum/2/
Must use `v-model.lazy` to bind works properly.
```html
<template>
  <div>
    <input v-model.lazy="price" v-money="money" /> {{price}}
  </div>
</template>

<script>
  import {VMoney} from 'v-money'

  export default {
    data () {
      return {
        price: 123.45,
        money: {
          decimal: ',',
          thousands: '.',
          prefix: 'R$ ',
          suffix: ' #',
          precision: 2,
          masked: false, /* doesn't work with directive */
          min: 0,
          max: 1000
        }
      }
    },

    directives: {money: VMoney}
  }
</script>
```

## Properties

| property   | Required | Type    | Default | Description                                             |
|------------|----------|---------|---------|---------------------------------------------------------|
| precision  | **true** | Number  | 2       | How many decimal places                                 |
| decimal    | false    | String  | "."     | Decimal separator                                       |
| thousands  | false    | String  | ","     | Thousands separator                                     |
| prefix     | false    | String  | ""      | Currency symbol followed by a Space, like "R$ "         |
| suffix     | false    | String  | ""      | Percentage for example: " %"                            |
| masked     | false    | Boolean | false   | If the component output should include the mask or not  |
| allowBlank | false    | Boolean | false   | If the field can start blank and be cleared out by user |
| min       | false    | Number  | Number.MIN_SAFE_INTEGER | The min value allowed                                   |
| max       | false    | Number  | Number.MAX_SAFE_INTEGER | The max value allowed                                   |

### References

- https://en.wikipedia.org/wiki/Decimal_mark
- https://docs.oracle.com/cd/E19455-01/806-0169/overview-9/index.html
- http://www.xe.com/symbols.php
- https://github.com/kevinongko/vue-numeric
- https://github.com/plentz/jquery-maskmoney
- https://github.com/vuejs-tips/v-money/pull/51
- https://github.com/vuejs-tips/v-money/pull/66
- https://github.com/vuejs-tips/v-money/pull/55
- https://github.com/vuejs-tips/v-money/pull/82
