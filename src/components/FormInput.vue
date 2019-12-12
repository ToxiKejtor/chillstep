<template>
  <div>
    <label :for="id">{{ label }}</label>
    <input
      :id="id"
      v-bind="$attrs"
      :type="type"
      :value="value"
      class="c-contact-form-input"
      @change="updateValue"
    />
  </div>
</template>

<script>
import getRandomId from "../utils/getRandomId";
export default {
  inheritAttrs: false,
  props: {
    value: {
      type: [String, Number],
      default: ""
    },
    type: {
      type: String,
      required: true
    },
    label: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      id: getRandomId(1, Math.pow(10, 8))
    };
  },
  methods: {
    updateValue(event) {
      this.$emit("input", event.target.value);
    }
  }
};
</script>

<style>
.c-contact-form-input {
  display: block;
  width: 100%;
  margin-bottom: 10px;
}
</style>
