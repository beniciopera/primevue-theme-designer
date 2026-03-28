<script setup lang="ts">
import { shallowRef, onMounted } from 'vue'
import Tabs from 'primevue/tabs'
import TabList from 'primevue/tablist'
import Tab from 'primevue/tab'
import TabPanels from 'primevue/tabpanels'
import TabPanel from 'primevue/tabpanel'
import Button from 'primevue/button'
import FormInputsDemo from './demo/FormInputsDemo.vue'
import DataDisplayDemo from './demo/DataDisplayDemo.vue'
import OverlayFeedbackDemo from './demo/OverlayFeedbackDemo.vue'
import MiscDemo from './demo/MiscDemo.vue'

const isDark = shallowRef(false)

onMounted(() => {
  isDark.value = window.matchMedia('(prefers-color-scheme: dark)').matches
  if (isDark.value) document.documentElement.classList.add('app-dark')
})

const toggleDark = () => {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('app-dark', isDark.value)
}
</script>

<template>
  <div class="demo-container">
    <header class="demo-header">
      <h1>PrimeVue 4 Component Demo</h1>
      <Button
        :icon="isDark ? 'pi pi-sun' : 'pi pi-moon'"
        :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
        text
        rounded
        @click="toggleDark"
      />
    </header>
    <Tabs value="0">
      <TabList>
        <Tab value="0">Form Inputs</Tab>
        <Tab value="1">Data Display</Tab>
        <Tab value="2">Overlay &amp; Feedback</Tab>
        <Tab value="3">Misc</Tab>
      </TabList>
      <TabPanels>
        <TabPanel value="0"><FormInputsDemo /></TabPanel>
        <TabPanel value="1"><DataDisplayDemo /></TabPanel>
        <TabPanel value="2"><OverlayFeedbackDemo /></TabPanel>
        <TabPanel value="3"><MiscDemo /></TabPanel>
      </TabPanels>
    </Tabs>
  </div>
</template>

<style scoped>
.demo-container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 1.5rem 2rem;
}

.demo-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1.5rem;
}

h1 {
  font-size: 2rem;
  font-weight: 600;
  margin: 0;
}
</style>
