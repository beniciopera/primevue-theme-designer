<script setup lang="ts">
import { ref, shallowRef } from 'vue'
import { useToast } from 'primevue/usetoast'
import Button from 'primevue/button'
import Dialog from 'primevue/dialog'
import Popover from 'primevue/popover'
import Drawer from 'primevue/drawer'
import Message from 'primevue/message'

const toast = useToast()
const dialogVisible = shallowRef(false)
const drawerVisible = shallowRef(false)
const popoverRef = ref<InstanceType<typeof Popover> | null>(null)

const showToast = (severity: 'success' | 'info' | 'warn' | 'error') => {
  toast.add({
    severity,
    summary: severity.charAt(0).toUpperCase() + severity.slice(1),
    detail: `This is a ${severity} toast message.`,
    life: 3000,
  })
}

const togglePopover = (event: Event) => {
  popoverRef.value?.toggle(event)
}
</script>

<template>
  <div class="demo-section">
    <section>
      <h2>Toast Notifications</h2>
      <div class="row wrap">
        <Button label="Success" severity="success" icon="pi pi-check" @click="showToast('success')" />
        <Button label="Info" severity="info" icon="pi pi-info-circle" @click="showToast('info')" />
        <Button label="Warning" severity="warn" icon="pi pi-exclamation-triangle" @click="showToast('warn')" />
        <Button label="Error" severity="danger" icon="pi pi-times-circle" @click="showToast('error')" />
      </div>
    </section>

    <section>
      <h2>Dialog (Modal)</h2>
      <Button label="Open Dialog" icon="pi pi-external-link" @click="dialogVisible = true" />
      <Dialog
        v-model:visible="dialogVisible"
        modal
        header="Example Dialog"
        :style="{ width: '26rem' }"
      >
        <p>This is a modal dialog. You can put any content here.</p>
        <p style="margin-top: 0.75rem">Click Confirm, Cancel, or the X to close it.</p>
        <template #footer>
          <Button label="Cancel" text severity="secondary" @click="dialogVisible = false" />
          <Button label="Confirm" @click="dialogVisible = false" />
        </template>
      </Dialog>
    </section>

    <section>
      <h2>Popover</h2>
      <Button label="Toggle Popover" icon="pi pi-info-circle" outlined @click="togglePopover" />
      <Popover ref="popoverRef">
        <div class="popover-content">
          <p><strong>Popover Panel</strong></p>
          <p>Triggered by a button click. Click outside to dismiss.</p>
          <ul>
            <li>Feature one</li>
            <li>Feature two</li>
            <li>Feature three</li>
          </ul>
        </div>
      </Popover>
    </section>

    <section>
      <h2>Drawer</h2>
      <Button label="Open Drawer" icon="pi pi-bars" outlined @click="drawerVisible = true" />
      <Drawer v-model:visible="drawerVisible" header="Side Drawer">
        <p>Drawer content slides in from the left side of the screen.</p>
        <p style="margin-top: 0.75rem">Great for navigation, filters, or detail panels.</p>
      </Drawer>
    </section>

    <section>
      <h2>Inline Messages</h2>
      <div class="messages">
        <Message severity="info">This is an informational message.</Message>
        <Message severity="success">Operation completed successfully.</Message>
        <Message severity="warn">Please review before proceeding.</Message>
        <Message severity="error">An error has occurred. Please try again.</Message>
      </div>
    </section>

    <section>
      <h2>Tooltip</h2>
      <div class="row wrap">
        <Button v-tooltip.top="'Tooltip on top'" label="Top" outlined />
        <Button v-tooltip.right="'Tooltip on right'" label="Right" outlined />
        <Button v-tooltip.bottom="'Tooltip on bottom'" label="Bottom" outlined />
        <Button v-tooltip.left="'Tooltip on left'" label="Left" outlined />
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

.row {
  display: flex;
  flex-direction: row;
  gap: 0.5rem;
}

.wrap {
  flex-wrap: wrap;
}

.messages {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  max-width: 500px;
}

.popover-content {
  padding: 0.5rem;
  min-width: 200px;
}

.popover-content p {
  margin: 0 0 0.5rem;
}

.popover-content ul {
  margin: 0.5rem 0 0;
  padding-left: 1.2rem;
}
</style>
