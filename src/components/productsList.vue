<template>

<!--  Filtering and sorting-->
  <div class="row text-center mb-3">
    <div class="col">
      <input type="text" class="form-control" id="filter" placeholder="Type to filter..." v-model="filterBy">
    </div>
    <div class="col">
      <select class="form-control" id="sort"  v-model="sortBy">
        <option disabled selected>Sort by...</option>
        <option value="asc">High Price First</option>
        <option value="desc">Low Price First</option>
      </select>
    </div>
  </div>

<!--  List of the items-->
  <div class="row">
    <div class="list col-auto border-end">
      <ul class="list-group text-start">
        <li v-for="item in handleFiltering" :key="item" :class="handleClass(item.id)"  @click="() => this.selectedId = item.id">
          {{ item.name }}
          <button class="btn btn-danger btn-sm" @click="$emit('deleteItem', item.id)">X</button>
        </li>
      </ul>
    </div>

<!--    Content of an item-->
    <div class="col">
      <h2 v-if="!selectedItem">Please choose product...</h2>
      <DetailsTable v-else :data="tableData" />
    </div>
  </div>

</template>

<script>
import * as _ from 'lodash'
import DetailsTable from '@/components/detailsTable'

export default {
  name: 'productList',
  components: { DetailsTable },
  emits: ['deleteItem'],
  props: {
    items: { type: Array, required: true }
  },
  data () {
    return {
      selectedId: 0,
      filterBy: '',
      sortBy: 'Sort by...',
      itemsFiltered: this.items
    }
  },
  computed: {
    handleClass () {
      return (id) => {
        const classes = 'list-group-item d-flex justify-content-between align-items-center '
        return classes + (this.selectedId === id ? 'active' : '')
      }
    },

    handleFiltering () {
      let filtering = this.items.filter(item => item.name.toLowerCase().includes(this.filterBy.toLowerCase()))
      if (this.sortBy !== 'Sort by...') {
        filtering = _.sortBy(filtering, 'price')
        return this.sortBy === 'asc' ? _.reverse(filtering) : filtering
      }
      return filtering
    },

    selectedItem () {
      return this.items.find(item => item.id === this.selectedId)
    },

    tableData () {
      const { name, description, price } = this.selectedItem
      return { name, description, price }
    }
  }
}
</script>

<style scoped>

.list {
  min-width: 250px
}

</style>
