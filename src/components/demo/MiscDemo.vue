<script setup lang="ts">
import { ref, shallowRef } from 'vue'
import Accordion from 'primevue/accordion'
import AccordionPanel from 'primevue/accordionpanel'
import AccordionHeader from 'primevue/accordionheader'
import AccordionContent from 'primevue/accordioncontent'
import Avatar from 'primevue/avatar'
import AvatarGroup from 'primevue/avatargroup'
import Chip from 'primevue/chip'
import Divider from 'primevue/divider'
import Knob from 'primevue/knob'
import Rating from 'primevue/rating'

const knobValue = shallowRef(40)
const ratingValue = shallowRef(3)
const chips = ref(['Vue 3', 'TypeScript', 'PrimeVue', 'Vite', 'Aura Theme'])

const removeChip = (chip: string) => {
  chips.value = chips.value.filter(c => c !== chip)
}
</script>

<template>
  <div class="demo-section">
    <section>
      <h2>Accordion</h2>
      <Accordion value="0">
        <AccordionPanel value="0">
          <AccordionHeader>Getting Started with PrimeVue</AccordionHeader>
          <AccordionContent>
            <p>PrimeVue is a rich UI component library for Vue.js. It offers 90+ components with the Aura, Lara, and Nora theme presets built in.</p>
          </AccordionContent>
        </AccordionPanel>
        <AccordionPanel value="1">
          <AccordionHeader>Component Categories</AccordionHeader>
          <AccordionContent>
            <p>PrimeVue components span form inputs, data display, overlays, menus, media, charts, and miscellaneous utilities — covering nearly every UI need.</p>
          </AccordionContent>
        </AccordionPanel>
        <AccordionPanel value="2">
          <AccordionHeader>Design Token Theming</AccordionHeader>
          <AccordionContent>
            <p>The Aura preset exposes design tokens you can override at the global, component, or element level without writing custom CSS.</p>
          </AccordionContent>
        </AccordionPanel>
      </Accordion>
    </section>

    <Divider />

    <section>
      <h2>Avatars</h2>
      <div class="row wrap align-center">
        <Avatar label="A" size="large" style="background-color: #ece9fc; color: #2a1261" />
        <Avatar label="BC" size="large" style="background-color: #fde68a; color: #92400e" />
        <Avatar icon="pi pi-user" size="large" />
        <Avatar icon="pi pi-star" size="large" style="background-color: #d1fae5; color: #065f46" shape="circle" />
        <Divider layout="vertical" style="height: 2.5rem" />
        <span style="font-size: 0.875rem; font-weight: 500">AvatarGroup:</span>
        <AvatarGroup>
          <Avatar label="P" style="background-color: #9c27b0; color: #ffffff" shape="circle" />
          <Avatar label="R" style="background-color: #2196f3; color: #ffffff" shape="circle" />
          <Avatar label="V" style="background-color: #4caf50; color: #ffffff" shape="circle" />
          <Avatar label="+2" shape="circle" />
        </AvatarGroup>
      </div>
    </section>

    <Divider />

    <section>
      <h2>Chips</h2>
      <div class="row wrap">
        <Chip
          v-for="chip in chips"
          :key="chip"
          :label="chip"
          removable
          @remove="removeChip(chip)"
        />
        <span v-if="chips.length === 0" style="font-size: 0.875rem; opacity: 0.6">All chips removed. Refresh to reset.</span>
      </div>
    </section>

    <Divider />

    <section>
      <h2>Knob &amp; Rating</h2>
      <div class="controls-row">
        <div class="control-item">
          <Knob v-model="knobValue" :size="100" />
          <span>Knob: {{ knobValue }}</span>
        </div>
        <div class="control-item">
          <Rating v-model="ratingValue" :stars="5" />
          <span>Rating: {{ ratingValue }} / 5</span>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.demo-section {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  padding: 1rem 0;
}

section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

h2 {
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid var(--p-surface-200);
}

.row {
  display: flex;
  flex-direction: row;
  gap: 0.5rem;
  align-items: center;
}

.wrap {
  flex-wrap: wrap;
}

.align-center {
  align-items: center;
}

.controls-row {
  display: flex;
  flex-direction: row;
  gap: 3rem;
  align-items: center;
  flex-wrap: wrap;
}

.control-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.875rem;
}
</style>
