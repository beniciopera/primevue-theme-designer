<script setup lang="ts">
import { ref, shallowRef } from 'vue'
import Button from 'primevue/button'
import InputText from 'primevue/inputtext'
import Textarea from 'primevue/textarea'
import Select from 'primevue/select'
import DatePicker from 'primevue/datepicker'
import InputNumber from 'primevue/inputnumber'
import Checkbox from 'primevue/checkbox'
import ToggleSwitch from 'primevue/toggleswitch'
import Password from 'primevue/password'
import FloatLabel from 'primevue/floatlabel'

const textValue = shallowRef('')
const textareaValue = shallowRef('')
const selectedCity = ref<{ name: string; code: string } | null>(null)
const dateValue = ref<Date | null>(null)
const numberValue = shallowRef(0)
const checked = shallowRef(false)
const toggled = shallowRef(false)
const password = shallowRef('')
const floatLabelValue = shallowRef('')

const cities = [
  { name: 'New York', code: 'NY' },
  { name: 'Rome', code: 'RM' },
  { name: 'London', code: 'LDN' },
  { name: 'Istanbul', code: 'IST' },
  { name: 'Paris', code: 'PRS' },
]
</script>

<template>
  <div class="demo-section">
    <section>
      <h2>Buttons</h2>
      <div class="row wrap">
        <Button label="Primary" />
        <Button label="Secondary" severity="secondary" />
        <Button label="Success" severity="success" />
        <Button label="Info" severity="info" />
        <Button label="Warning" severity="warn" />
        <Button label="Danger" severity="danger" />
        <Button label="Outlined" outlined />
        <Button label="Text" text />
        <Button icon="pi pi-check" aria-label="Check" rounded />
        <Button icon="pi pi-search" label="Search" />
        <Button icon="pi pi-upload" label="Upload" iconPos="right" />
        <Button label="Loading" loading />
      </div>
    </section>

    <section>
      <h2>Text Inputs</h2>
      <div class="form-grid">
        <div class="field">
          <label>InputText</label>
          <InputText v-model="textValue" placeholder="Type something..." class="w-full" />
        </div>
        <div class="field">
          <label>Password</label>
          <Password v-model="password" placeholder="Enter password" :feedback="true" class="w-full" />
        </div>
        <div class="field">
          <FloatLabel>
            <InputText id="floatlabel" v-model="floatLabelValue" class="w-full" />
            <label for="floatlabel">Float Label</label>
          </FloatLabel>
        </div>
        <div class="field">
          <label>Textarea</label>
          <Textarea v-model="textareaValue" rows="3" placeholder="Enter text..." class="w-full" />
        </div>
      </div>
    </section>

    <section>
      <h2>Selection Inputs</h2>
      <div class="form-grid">
        <div class="field">
          <label>Select (Dropdown)</label>
          <Select
            v-model="selectedCity"
            :options="cities"
            optionLabel="name"
            placeholder="Select a City"
            class="w-full"
          />
        </div>
        <div class="field">
          <label>DatePicker</label>
          <DatePicker v-model="dateValue" placeholder="Select a date" class="w-full" />
        </div>
        <div class="field">
          <label>InputNumber</label>
          <InputNumber v-model="numberValue" showButtons class="w-full" />
        </div>
      </div>
    </section>

    <section>
      <h2>Toggles</h2>
      <div class="row">
        <div class="row align-center">
          <Checkbox v-model="checked" inputId="cb1" :binary="true" />
          <label for="cb1">Checkbox ({{ checked }})</label>
        </div>
        <div class="row align-center">
          <ToggleSwitch v-model="toggled" />
          <label>Toggle Switch ({{ toggled }})</label>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.demo-section {
  display: flex;
  flex-direction: column;
  gap: 2rem;
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

.wrap {
  flex-wrap: wrap;
}

.align-center {
  align-items: center;
}

.form-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 1rem;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.field label {
  font-size: 0.875rem;
  font-weight: 500;
}

.w-full {
  width: 100%;
}
</style>
