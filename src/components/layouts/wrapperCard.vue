<template>
  <div id="card-container" class="align-content-center">
    <div class="card" :style="'min-width:' + (width || '100%')">
      <div v-if="header" class="card-header text-start">{{header}}</div>
      <div class="card-body">
        <div class="card-text text-start">
          <slot />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'wrapperCard',
  props: {
    header: String,
    width: String
  }
}
</script>

<style scoped>
#card-container {
  display: flex;
  justify-content: center;
}
</style>
