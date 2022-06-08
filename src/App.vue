<template>
<div class="container">

  <h1 class="mb-4">Products List</h1>

  <div class="row">
    <WrapperCard header="Add product" width="650px" class="mb-5">
      <ProductsForm @addItem="addItem" :esists="items" />
    </WrapperCard>
  </div>

  <div class="row">
    <WrapperCard width="850px">
      <ProductsList :items="items" @deleteItem="deleteItem" />
    </WrapperCard>
  </div>

</div>
</template>

<script>

import WrapperCard from '@/components/layouts/wrapperCard'
import ProductsForm from '@/components/productsForm'
import ProductsList from '@/components/productsList'

export default {
  name: 'App',
  components: { ProductsList, ProductsForm, WrapperCard },
  data () {
    return {
      counter: 0,
      items: []
    }
  },
  methods: {
    deleteItem (id) {
      this.items = this.items.filter(item => item.id !== id)
    },
    addItem (item) {
      this.items.push({ id: ++this.counter, ...item })
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
