# Vue Tips

Some of the tips uses [Quasar](https://quasar.dev/) methods, as most of my projects use it to accelerate development.

## Dark Mode (Quasar)

A implementation of optional dark mode using [Quasar Dark Plugin](https://quasar.dev/quasar-plugins/dark).

The app will save on Local Storage the user choice about dark mode and load the choices on start up, if there's no user choice present, fallback to OS preferences.

```js
// darkMode.js

import { Dark } from 'quasar';

const DARK_MODE_ACTIVE = 'dark-mode-active';

const mapValue = val => (val ? 1 : 0);

/**
 * Get dark mode from localstorage or current app mode
 *
 * @returns {boolean} If dark mode is enabled
 */
const getActiveStatus = () => {
  const result = localStorage.getItem(DARK_MODE_ACTIVE);
  return result ? Boolean(Number(result)) : true;
};

/**
 * Save dark mode status on local storage and update current app mode
 *
 * @param {boolean} val dark mode status
 */
export const setActiveStatus = (val) => {
  localStorage.setItem(DARK_MODE_ACTIVE, mapValue(val));
  Dark.set(val);
};

export const setLastStatus = () => {
  const active = getActiveStatus();
  setActiveStatus(active);
};
```

A Component using custom background colors, what require custom CSS classes based on the current app mode.

```vue
// Component.vue

<template>
  <div class="bg-color">
    ...
  </div>
</template>

<style lang="stylus">
  .body--light
    .bg-color
      background-color white
  .body--dark
    .bg-color
      background-color black
</style>

```

App load user choices on startup

```vue
// App.vue

<script>
import { setLastStatus } from 'src/helpers/darkMode';

export default {
  beforeMount() {
    setLastStatus();
  },
};
</script>

```

A simple settings component

```vue
<template>
  ...
  <q-item
    v-ripple
    tag="label"
  >
    <q-item-section>
      <q-item-label>Dark Mode</q-item-label>
    </q-item-section>
    <q-item-section
      side
      top
    >
      <q-toggle
        :value="darkModeActive"
        @input="changeDarkMode"
      />
    </q-item-section>
  </q-item>
  ...
</template>

<script>
import { setActiveStatus } from 'src/helpers/darkMode';

export default {
  computed: {
    darkModeActive() {
      return this.$q.dark.isActive;
    },
  },

  methods: {
    changeDarkMode(val) {
      setActiveStatus(val);
    },
  },
};
</script>
```
