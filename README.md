# Vue-flatPickr

[![vue-js](https://img.shields.io/badge/vue.js-2.x-brightgreen.svg?maxAge=604800)](https://vuejs.org/)
[![downloads](https://img.shields.io/npm/dt/vue-flatpickr-component.svg)](http://npm-stats.com/~packages/vue-flatpickr-component)
[![npm-version](https://img.shields.io/npm/v/vue-flatpickr-component.svg)](https://www.npmjs.com/package/vue-flatpickr-component)
[![github-tag](https://img.shields.io/github/tag/ankurk91/vue-flatpickr-component.svg?maxAge=1800)](https://github.com/ankurk91/vue-flatpickr-component/)
[![license](https://img.shields.io/github/license/ankurk91/vue-flatpickr-component.svg?maxAge=1800)](https://yarnpkg.com/en/package/vue-flatpickr-component)
[![build-status](https://travis-ci.org/ankurk91/vue-flatpickr-component.svg?branch=master)](https://travis-ci.org/ankurk91/vue-flatpickr-component)
[![codecov](https://codecov.io/gh/ankurk91/vue-flatpickr-component/branch/master/graph/badge.svg)](https://codecov.io/gh/ankurk91/vue-flatpickr-component)

Vue.js v2.x component for [Flatpickr](https://chmln.github.io/flatpickr/) date-time picker

:point_right: This branch is only for v4.x, [click here](https://github.com/ankurk91/vue-flatpickr-component/tree/v3.x) for Flatpickr v3.x

## Demo on [JSFiddle](https://jsfiddle.net/ankurk91/63kzdwLx/)

## Features
* Reactive ``v-model`` value
    - You can change flatpickr value programmatically 
* Reactive [config](https://chmln.github.io/flatpickr/options/) options
    - You can change config options dynamically
    - Component will watch for any changes and redraw itself
    - You are suggested to modify config via [Vue.set](https://vuejs.org/v2/api/#Vue-set)
* Compatible with [Bootstrap](http://getbootstrap.com/), [Bulma](http://bulma.io/) or any other CSS framework
* Supports [wrapped](https://chmln.github.io/flatpickr/examples/#flatpickr-external-elements) mode
    - Just set ``wrap:true`` in config and component will take care of all
* Play nice with [vee-validate](https://github.com/logaretm/vee-validate) validation library

## Installation
```bash
# npm
npm install vue-flatpickr-component --save

# Yarn
yarn add vue-flatpickr-component
```

## Usage
#### Minimal example
```html
<template>
  <div>
    <flat-pickr v-model="date"></flat-pickr>
  </div>
</template>

<script>
  import flatPickr from 'vue-flatpickr-component';
  import 'flatpickr/dist/flatpickr.css';
  
  export default {    
    data () {
      return {
        date: null,       
      }
    },
    components: {
      flatPickr
    }
  }
</script>
```

#### Detailed example
This example is based on Bootstrap 4 [input group](https://getbootstrap.com/docs/4.0/components/input-group/)
```html
<template>
  <section>
    <div class="form-group">
      <label>Select a date</label>
      <div class="input-group">
        <flat-pickr
                v-model="date"
                placeholder="Select date"
                :config="config"
                :required="true"                
                input-class="form-control custom-input-class"                
                name="date">
        </flat-pickr>
        <div class="input-group-btn">
          <button class="btn btn-default" type="button" title="Toggle" data-toggle>
            <i class="fa fa-calendar">
              <span aria-hidden="true" class="sr-only">Toggle</span>
            </i>
          </button>
        </div>
      </div>
    </div>
    <pre>Selected date is - {{date}}</pre>
  </section>
</template>

<script>
  // bootstrap is just for this example
  import 'bootstrap/dist/css/bootstrap.css';
  // import this component
  import flatPickr from 'vue-flatpickr-component';  
  import 'flatpickr/dist/flatpickr.css';
  // theme is optional
  import 'flatpickr/dist/themes/material_blue.css';
  // l10n is optional
  import {Hindi} from 'flatpickr/dist/l10n/hi';
  
  export default {
    name: 'yourComponent',
    data () {
      return {
        // Initial value
        date: new Date(),
        // Get more form https://chmln.github.io/flatpickr/options/
        config: {
          wrap: true, // set wrap to true when using 'input-group'
          altFormat: 'M	j, Y',
          altInput: true,
          dateFormat: "Y-m-d",
          locale: Hindi, // locale for this instance only          
        },                
      }
    },
    components: {
      flatPickr
    },    
  }
</script>
```

#### As plugin
```js
  import Vue from 'vue';
  import flatPickr from 'vue-flatpickr-component';
  import 'flatpickr/dist/flatpickr.css';
  Vue.use(flatPickr);
```
This will register a global component `<flat-pickr>`

## Available props
The component accepts these props:

| Attribute        | Type                               | Default              | Description      |
| :---             | :---:                              | :---:                | :---             |
| v-model / value  | String / Date Object / Array / null| `null`               | Set or Get date-picker value (required) |
| config           | Object                             | `{wrap:false}`       | Flatpickr configuration [options](https://chmln.github.io/flatpickr/options/)|
| placeholder      | String                             | `''`                 | Set placeholder on input field |
| input-class      | String / Object                    | `'form-control input'` | Set CSS class on input field |
| name             | String                             | `'date-time'`        | Set input field name  |
| required         | Boolean                            | `false`              | Make input field required |
| id               | String                             | `''`                 | Set input field id  |

## Install in non-module environments (without webpack)
* Include required files
```html
<!-- Flatpickr related files -->
<link href="https://unpkg.com/flatpickr@4/dist/flatpickr.min.css" rel="stylesheet">
<script src="https://unpkg.com/flatpickr@4/dist/flatpickr.min.js"></script>
<!-- Vue js -->
<script src="https://unpkg.com/vue@2.5/dist/vue.min.js"></script>
<!-- Lastly add this package -->
<script src="https://unpkg.com/vue-flatpickr-component"></script>
```
* Use the component anywhere in your app like this
```html
<main id="app">  
    <flat-pickr v-model="date"></flat-pickr> 
</main>
<script>
  //Initialize as global component
  Vue.component('flat-pickr', VueFlatpickr.default);
  
  new Vue({
    el: '#app',
    data: {
      date: null
    },    
  });
</script>
```

## Run examples on your localhost
* Clone this repo
* You should have node-js >=6.10 and yarn >=1.x pre-installed
* Install dependencies
``
yarn install
``
* Run webpack dev server
``
yarn start
``
* This should open the demo page at ``http://localhost:8080`` in your default web browser

### Testing
* This package is using [Jest](https://github.com/facebook/jest) and [vue-test-utils](https://github.com/vuejs/vue-test-utils) for testing.
* Tests can be found in `__test__` folder.
* Execute tests with this command
```bash
yarn test
```

## Changelog
Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## License
[MIT](LICENSE.txt) License
