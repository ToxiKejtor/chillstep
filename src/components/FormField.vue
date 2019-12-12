<template>
  <div class="c-form-field">
    <label class="c-form-field__label" :for="id">{{ label }}</label>
    <slot />
  </div>
</template>

<script>
export default {
  name: "FormField",
  props: {
    label: {
      type: String,
      default: ""
    },
    id: {
      type: [String, Number],
      required: true
    }
  }
};
</script>

<style>
.c-form-field {
  margin-bottom: 15px;
}

.c-form-field__label {
  display: block;
  text-align: left;
  margin-bottom: 5px;
}
</style>
