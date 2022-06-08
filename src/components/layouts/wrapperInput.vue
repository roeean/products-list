<template>
  <div class="row mb-3 align-items-center">

    <label :for="id" class="col-form-label col-2 text-start">
      {{ label }}
    </label>

    <div class="col-5 text-start">
      <slot :id="id" />
    </div>

    <div v-if="helper" class="col-5 text-start">
      <span class="form-text" :id="id + 'Helper'">{{helper}}</span>
    </div>

  </div>
</template>

<script>
export default {
  name: 'wrapperInput',
  props: {
    id: { required: true, type: String },
    label: { required: true, type: String },
    helper: String
  }
}
</script>
