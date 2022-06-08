<template>
  <form>

    <div class="row">
      <div class="col">

        <wrapperInput id="name" label="Name" helper="Must be up to 20 characters" v-slot="slotProps">
          <input :id="slotProps.id" class="form-control" type="text" v-model="item.name" maxlength="20" />
        </wrapperInput>

        <wrapperInput id="description" label="Description" helper="Describe the product" v-slot="slotProps">
          <input :id="slotProps.id" class="form-control" type="text" v-model="item.description" />
        </wrapperInput>

        <wrapperInput id="price" label="Price" helper="In Dollars" v-slot="slotProps">
          <input :id="slotProps.id" class="form-control" type="number" v-model="item.price" />
        </wrapperInput>

      </div>
    </div>

    <div class="row">
      <div class="col text-end">
        <button type="button" :class="'btn btn-primary ' + (validateForm || 'disabled')" @click="addItem(item)">Push to the list</button>
      </div>
    </div>

  </form>
</template>

<script>
import wrapperInput from '@/components/layouts/wrapperInput'

export default {
  name: 'productForm',
  components: { wrapperInput },
  emits: ['addItem'],
  data () {
    return {
      item: { name: '', description: '', price: '' }
    }
  },
  methods: {
    addItem (item) {
      this.$emit('addItem', item)
      this.item = { name: '', description: '', price: '' }
    }
  },
  computed: {
    validateForm () {
      const { item } = this
      return (item.name !== '' && item.description !== '' && item.price !== '')
    }
  }
}
</script>
