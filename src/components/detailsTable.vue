<template>
  <table class="table text-start">
    <tbody>
    <tr v-for="item in Object.keys(data)" :key="item.label">
      <th>{{item}}</th>
      <td>{{data[item]}}</td>
    </tr>

    </tbody>
  </table>
</template>

<script>
export default {
  name: 'DetailsTable',
  props: {
    data: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
  th { width: 30% }
  td { width: 70% }
</style>
