Toggle
=======

> A simple UI state toggle for Vue.js

With a simple toggle, you can build almost any UI experience. Think about experiences like show/hide, accordions, nested menus, and even sliders, they mostly revolve around a single piece of state.

## Demo

Check out [the website for demos](https://james2doyle.github.io/vue-toggle).

## Installation

```bash
npm install -S vue-ui-toggle
```

```javascript
const Toggle = require('vue-ui-toggle'); // es5/node
// import Toggle from 'vue-ui-toggle'; // es6

Vue.component('toggle', Toggle);
```

```javascript
import Toggle from 'vue-ui-toggle';

export default {
  // ...
  components: {
    Toggle,
  },
  // ...
};
```

## Bindings

- `toggle` `Function<void>`: flip the state of the toggle
- `state` `string | number | boolean | null>`: the state of the toggle (default `null`)
- `setState` `Function(state: string | number | boolean | null): void`: set the state to something that isnt a boolean

## Examples

**Example: show/hide**

```html
<toggle #default="{ state, toggle }">
  <p v-if="state === false">I am showing by default</p>
  <p v-else>I will show when state is true</p>
  <button type="button" @click.prevent="toggle">Toggle State</button>
</toggle>
```

**Example: show/hide with transitions**

```html
<toggle #default="{ state, toggle }">
  <transition name="fade">
    <p v-if="state === false">I am showing by default</p>
    <p v-else>I will show when state is true</p>
  </transition>
  <button type="button" @click.prevent="toggle">Toggle State</button>
</toggle>
```

**Example: accordion**

```html
<toggle #default="{ state, setState }">
  <div class="accordion">
    <button type="button" @click="setState('tab-1')">Tab 1</button>
    <button type="button" @click="setState('tab-2')">Tab 2</button>
    <button type="button" @click="setState('tab-3')">Tab 3</button>
    <div v-if="state === 'tab-1'">Content for tab-1</div>
    <div v-if="state === 'tab-2'">Content for tab-2</div>
    <div v-if="state === 'tab-3'">Content for tab-3</div>
  </div>
</toggle>
```

**Example: nested toggles**

```html
<toggle #default="{ state, toggle }">
  <button type="button" @click.prevent="toggle">Next Level</button>
  <div v-if="state">
    <p>I am nested at level 1</p>
    <toggle #default="{ state, toggle }">
      <button type="button" @click.prevent="toggle">Next Level</button>
      <div v-if="state">
        <p>I am nested at level 2</p>
        <toggle #default="{ state, toggle }">
          <button type="button" @click.prevent="toggle">Next Level</button>
          <div v-if="state">
            <p>I am nested at level 3</p>
            <toggle #default="{ state, toggle }">
              <button type="button" @click.prevent="toggle">Next Level</button>
              <div v-if="state">
                <p>I am nested at level 4</p>
              </div>
            </toggle>
          </div>
        </toggle>
      </div>
    </toggle>
  </div>
</toggle>
```

**Example: slider**

```html
<toggle #default="{ state, setState }" :initial-state="0">
  <transition-group name="slider" tag="div" class="slider-wrapper">
    <div :key="0" v-show="state === 0">
      <img class="slider-image" src="https://placehold.it/400x250?text=slide+0" />
    </div>
    <div :key="1" v-show="state === 1">
      <img class="slider-image" src="https://placehold.it/400x250?text=slide+1" />
    </div>
    <div :key="2" v-show="state === 2">
      <img class="slider-image" src="https://placehold.it/400x250?text=slide+2" />
    </div>
  </transition-group>
  <div class="slider-controls">
    <button type="button" @click="setState(state - 1 < 0 ? 0 : state - 1)">Back</button>
    <button type="button" @click="setState(state + 1 > 2 ? 2 : state + 1)">Next</button>
  </div>
</toggle>
```
