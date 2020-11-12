<template>
  <div class="toggle-wrapper">
    <slot v-bind="{ state, toggle, setState }"></slot>
  </div>
</template>

<script>
export default {
  name: 'Toggle',
  props: {
    /** @type {String, Number, Boolean, null} */
    initialState: {
      type: [String, Number, Boolean, null],
      required: false,
      default: null,
    },
  },
  data() {
    return {
      /** @type {String, Number, Boolean, null} */
      state: false,
    };
  },
  mounted() {
    if (this.initialState !== null) {
      this.setState(this.initialState);
    }
  },
  methods: {
    toggle() {
      if (typeof this.state !== 'boolean') {
        console.warn('Vue Toggle: `toggle` function called on state that is not a boolean');
      }

      this.state = !Boolean(this.state);
    },
    setState(state) {
      this.state = state;
    },
  }
};
</script>
