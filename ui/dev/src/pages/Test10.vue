<template>
  <q-page padding>
    <q-btn @click="selected=[]" label="Clear Selection"></q-btn>

    <q-grid :data="data" :columns="columns" :columns_filter="true" :draggable="true" selection="multiple"
            :csv_download="true" file_name="sample" :groupby_filter="true"
            :selected="selected"
            @selected-val="GetSelected($event)">
      <template v-slot:header="props">
        <q-tr :props="props">
          <q-th auto-width></q-th>
          <q-th
            v-for="col in props.cols"
            class="text-italic text-purple"
          >
            {{ col.label }}
          </q-th>
        </q-tr>
      </template>
      <template v-slot:top_right="props">
        {{props}}
        <q-input
          v-if="props.global_search"
          v-model="props.filter"
          filled
          borderless
          dense
          debounce="300"
          class="q-mr-md"
          placeholder="Search"
        >
          <template v-slot:append>
            <q-icon name="search"/>
          </template>
        </q-input>

        <q-btn
          v-if="props.excel_download"
          class="bg-grey-2 q-mr-sm"
          icon="fas fa-file-excel"
          no-caps
          @click="props.exportTable('xlsx')"
        />

        <q-btn
          v-if="props.csv_download"
          class="bg-primary text-white"
          icon="fas fa-file-csv"
          no-caps
          @click="props.exportTable('csv')"
        />

        <q-select
          v-if="props.groupby_filter"
          class="q-mr-sm q-ml-sm"
          outlined
          dense
          v-model="props.selected_group_by_filed"
          :options="props.gorupby_option"
          style="width: 150px;"
        />

<!--        <q-btn-->
<!--          v-if="props.fullscreen"-->
<!--          flat-->
<!--          round-->
<!--          dense-->
<!--          class="q-ml-sm"-->
<!--          :icon="props.inFullscreen ? 'fullscreen_exit' : 'fullscreen'"-->
<!--          @click="props.toggleFullscreen"-->
<!--        >-->
<!--          <q-tooltip :disable="$q.platform.is.mobile" v-close-popup>-->
<!--            {{ props.inFullscreen ? 'Exit Fullscreen' : 'Toggle Fullscreen' }}-->
<!--          </q-tooltip>-->
<!--        </q-btn>-->
      </template>
    </q-grid>
    {{selected}}
  </q-page>
</template>

<style lang="sass" scoped>
.directive-target
  width: 50px
  height: 50px
</style>

<script>

import {defineComponent, ref} from 'vue';

const columns = [
  {
    name: 'name',
    required: true,
    label: 'Dessert (100g serving)',
    align: 'left',
    field: 'name',
    sortable: true,
    grouping: true
  },
  {name: 'calories', align: 'center', label: 'Calories', field: 'calories', sortable: true, grouping: true},
  {name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true},
  {name: 'carbs', label: 'Carbs (g)', field: 'carbs'},
  {name: 'protein', label: 'Protein (g)', field: 'protein'},
  {name: 'sodium', label: 'Sodium (mg)', field: 'sodium'},
  {
    name: 'calcium',
    label: 'Calcium (%)',
    field: 'calcium',
    sortable: true,
    sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
  },
  {
    name: 'iron',
    label: 'Iron (%)',
    field: 'iron',
    sortable: true,
    sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
  }
]
const data = [
  {
    name: 'Frozen Yogurt',
    calories: 159,
    fat: 6.0,
    carbs: 24,
    protein: 4.0,
    sodium: 87,
    calcium: '14%',
    iron: '1%'
  },
  {
    name: 'Ice cream sandwich',
    calories: 237,
    fat: 9.0,
    carbs: 37,
    protein: 4.3,
    sodium: 129,
    calcium: '8%',
    iron: '1%'
  },
  {
    name: 'Eclair',
    calories: 262,
    fat: 16.0,
    carbs: 23,
    protein: 6.0,
    sodium: 337,
    calcium: '6%',
    iron: '7%'
  },
  {
    name: 'Cupcake',
    calories: 305,
    fat: 3.7,
    carbs: 67,
    protein: 4.3,
    sodium: 413,
    calcium: '3%',
    iron: '8%'
  },
  {
    name: 'Gingerbread',
    calories: 356,
    fat: 16.0,
    carbs: 49,
    protein: 3.9,
    sodium: 327,
    calcium: '7%',
    iron: '16%'
  },
  {
    name: 'Jelly bean',
    calories: 375,
    fat: 0.0,
    carbs: 94,
    protein: 0.0,
    sodium: 50,
    calcium: '0%',
    iron: '0%'
  },
  {
    name: 'Lollipop',
    calories: 392,
    fat: 0.2,
    carbs: 98,
    protein: 0,
    sodium: 38,
    calcium: '0%',
    iron: '2%'
  },
  {
    name: 'Honeycomb',
    calories: 408,
    fat: 3.2,
    carbs: 87,
    protein: 6.5,
    sodium: 562,
    calcium: '0%',
    iron: '45%'
  },
  {
    name: 'Donut',
    calories: 452,
    fat: 25.0,
    carbs: 51,
    protein: 4.9,
    sodium: 326,
    calcium: '2%',
    iron: '22%'
  },
  {
    name: 'KitKat',
    calories: 518,
    fat: 26.0,
    carbs: 65,
    protein: 7,
    sodium: 54,
    calcium: '12%',
    iron: '6%'
  }
]
export default defineComponent({
  name: 'Test10',
  setup() {
    return {
      data,
      columns,
      selected: ref([]),
      GetSelected(Selected) {
        this.selected = Selected
        console.log(Selected)
        console.log(this.selected)
      }
    }
  }
})
</script>
