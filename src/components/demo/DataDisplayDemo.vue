<script setup lang="ts">
import { shallowRef } from 'vue'
import DataTable from 'primevue/datatable'
import Column from 'primevue/column'
import Card from 'primevue/card'
import Tag from 'primevue/tag'
import Badge from 'primevue/badge'
import ProgressBar from 'primevue/progressbar'
import Button from 'primevue/button'

interface Product {
  id: number
  name: string
  category: string
  price: number
  status: 'instock' | 'lowstock' | 'outofstock'
}

const products: Product[] = [
  { id: 1, name: 'Bamboo Watch', category: 'Accessories', price: 65, status: 'instock' },
  { id: 2, name: 'Black Watch', category: 'Accessories', price: 72, status: 'instock' },
  { id: 3, name: 'Blue Band', category: 'Fitness', price: 79, status: 'lowstock' },
  { id: 4, name: 'Blue T-Shirt', category: 'Clothing', price: 29, status: 'instock' },
  { id: 5, name: 'Bracelet', category: 'Accessories', price: 15, status: 'outofstock' },
]

const selectedProducts = shallowRef<Product[]>([])

const statusSeverity = (status: Product['status']) => {
  switch (status) {
    case 'instock': return 'success'
    case 'lowstock': return 'warn'
    case 'outofstock': return 'danger'
  }
}
</script>

<template>
  <div class="demo-section">
    <section>
      <h2>DataTable</h2>
      <DataTable
        :value="products"
        v-model:selection="selectedProducts"
        selectionMode="multiple"
        :metaKeySelection="false"
        sortMode="multiple"
        removableSort
        tableStyle="min-width: 40rem"
      >
        <Column selectionMode="multiple" headerStyle="width: 3rem" />
        <Column field="id" header="ID" sortable style="width: 4rem" />
        <Column field="name" header="Name" sortable />
        <Column field="category" header="Category" sortable />
        <Column field="price" header="Price" sortable>
          <template #body="{ data }">
            ${{ data.price }}
          </template>
        </Column>
        <Column field="status" header="Status">
          <template #body="{ data }">
            <Tag :value="data.status" :severity="statusSeverity(data.status)" />
          </template>
        </Column>
      </DataTable>
    </section>

    <section>
      <h2>Cards</h2>
      <div class="card-grid">
        <Card>
          <template #title>Simple Card</template>
          <template #content>
            <p>Cards are flexible containers for related content and actions.</p>
          </template>
          <template #footer>
            <div class="row gap">
              <Button label="Cancel" text severity="secondary" />
              <Button label="Save" />
            </div>
          </template>
        </Card>
        <Card>
          <template #header>
            <div class="card-header-image" />
          </template>
          <template #title>Card with Header</template>
          <template #subtitle>Subtitle text</template>
          <template #content>
            <p>This card has a colored header area at the top.</p>
          </template>
        </Card>
        <Card>
          <template #title>Tag Variants</template>
          <template #content>
            <div class="row wrap gap">
              <Tag value="Success" severity="success" />
              <Tag value="Info" severity="info" />
              <Tag value="Warning" severity="warn" />
              <Tag value="Danger" severity="danger" />
              <Tag value="Default" />
            </div>
          </template>
        </Card>
      </div>
    </section>

    <section>
      <h2>Badges</h2>
      <div class="row wrap gap align-center">
        <Badge value="4" />
        <Badge value="8" severity="secondary" />
        <Badge value="12" severity="info" />
        <Badge value="2" severity="success" />
        <Badge value="5" severity="warn" />
        <Badge value="99+" severity="danger" />
      </div>
    </section>

    <section>
      <h2>ProgressBar</h2>
      <div class="progress-list">
        <div class="field">
          <span>75% complete</span>
          <ProgressBar :value="75" />
        </div>
        <div class="field">
          <span>40% complete</span>
          <ProgressBar :value="40" />
        </div>
        <div class="field">
          <span>Indeterminate</span>
          <ProgressBar mode="indeterminate" style="height: 6px" />
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

.row {
  display: flex;
  flex-direction: row;
}

.wrap {
  flex-wrap: wrap;
}

.gap {
  gap: 0.5rem;
}

.align-center {
  align-items: center;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1rem;
}

.card-header-image {
  background: var(--p-primary-color);
  height: 80px;
  border-radius: 6px 6px 0 0;
}

.progress-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 500px;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.field span {
  font-size: 0.875rem;
}
</style>
