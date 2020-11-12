<template>
  <div id="app" class="container">
    <h3>Example: show/hide</h3>

    <toggle #default="{ state, toggle }">
      <p v-if="state === false">I am showing by default</p>
      <p v-else>I will show when state is true</p>
      <button type="button" @click.prevent="toggle">Toggle State</button>
    </toggle>

    <h3>Example: show/hide with transitions</h3>

    <toggle #default="{ state, toggle }">
      <transition name="fade" appear>
        <p v-if="state === false">I am showing by default</p>
        <p v-else>I will show when state is true</p>
      </transition>
      <button type="button" @click.prevent="toggle">Toggle State</button>
    </toggle>

    <h3>Example: accordion</h3>

    <toggle #default="{ state, setState }">
      <div class="accordion">
        <button type="button" @click="setState('tab-1')">Tab 1</button>&nbsp;
        <button type="button" @click="setState('tab-2')">Tab 2</button>&nbsp;
        <button type="button" @click="setState('tab-3')">Tab 3</button>
        <div v-if="state === 'tab-1'">Content for tab-1</div>
        <div v-if="state === 'tab-2'">Content for tab-2</div>
        <div v-if="state === 'tab-3'">Content for tab-3</div>
      </div>
    </toggle>

    <h3>Example: nested toggles</h3>

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

    <h3>Example: slider</h3>

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
        <button type="button" @click="setState(state - 1 < 0 ? 0 : state - 1)">Back</button>&nbsp;
        <button type="button" @click="setState(state + 1 > 2 ? 2 : state + 1)">Next</button>
      </div>
    </toggle>
  </div>
</template>

<script>
import Vue from 'vue';
import Toggle from '@/toggle.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    Toggle
  }
});
</script>

<style>
.container {
  width: 100%;
  max-width: 800px;
  margin: 2rem auto 5rem;
  padding: 0 2rem;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s ease;
  will-change: opacity;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slider-wrapper {
  position: relative;
  width: 400px;
  height: 250px;
  overflow: visible;
}

.slider-image {
  position: absolute;
  top: 0;
  left: 0;
  vertical-align: top;
}

.slider-enter-active, .slider-leave-active {
  transition: all 1s;
  will-change: opacity, transform;
}

.slider-enter {
  opacity: 0;
  transform: translateX(100%);
}

.slider-leave-to {
  opacity: 0;
  transform: translateX(-100%);
}
</style>
