<template>
  <div id="app">
    <NuxtLayout :name="layout">
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script lang="ts" setup>
import { registerSW } from 'virtual:pwa-register'
import 'devicon'

registerSW()
/* -- type, interface -- */

/* -- store -- */
const colorStore = useColorStore()
const displayStatusStore = useDisplayStatusStore()
const colorModeStore = useColorModeStore()
const productDataStore = useProductDataStore()

/* -- props, emit -- */

/* -- variable(ref, reactive, computed) -- */
const nuxtApp = useNuxtApp()
const loading = ref(false)
const layout = computed(() => {
  if (useRoute().fullPath === '/') {
    return 'top'
  } else if (displayStatusStore.displaySize === 'sm') {
    return 'smartphone'
  } else {
    return 'default'
  }
})

useSvh()

/* -- function -- */

/* -- watch -- */

/* -- life cycle -- */
nuxtApp.hook('page:start', () => {
  loading.value = true
})
nuxtApp.hook('page:finish', () => {
  loading.value = false
})
productDataStore.getProductData()
</script>

<style lang="scss">
:root {
  --svh: 1vh
}

html, body {
  margin: 0px;

  font-family: 'Noto Sans JP', sans-serif;

  ::-webkit-scrollbar {
    width: 8px;
    height: 8px;
  }

  ::-webkit-scrollbar-track {
    background-color: transparent;
    border-radius: 2px;
  }

  ::-webkit-scrollbar-thumb {
    border: 2px solid transparent;
    border-radius: 8px;
    background-color: v-bind("colorModeStore.colorMode === 'dark' ? colorStore.color.black.lighten[1] : colorStore.color.black.lighten[1]");
    background-clip: content-box;
  }

  ::-webkit-scrollbar-corner {
    display: none;
  }
}

#app {
  width: 100vw;
  height: 100vh;
  height: calc(var(--svh, 1vh) * 100);
  max-height: calc(var(--svh, 1vh) * 100);
  background-color: v-bind("colorStore.color.theme.background");
  color: v-bind("colorStore.color.theme.text");
}

p {
  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 400;
}

hr {
  border: none;
  border-bottom: solid 1px v-bind("colorModeStore.colorMode === 'dark' ? colorStore.color.black.lighten[1] : colorStore.color.black.lighten[2]");
}

.loading {
  position: absolute;
  width: 100vw;
  height: 100vh;
  height: calc(var(--svh, 1vh) * 100);
  max-height: calc(var(--svh, 1vh) * 100);
  top: 0%;
  left: 0%;

  background-color: v-bind("colorStore.color.theme.background");
}
</style>
