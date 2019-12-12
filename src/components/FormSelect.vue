<template>
  <FormField :id="id" :label="label">
    <select
      :id="id"
      v-bind="$attrs"
      class="c-form-select"
      :value="value"
      @change="updateValue($event.target.value)"
    >
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
      >
        {{ option.text }}
      </option>
    </select>
  </FormField>
</template>

<script>
import getRandomId from "../utils/getRandomId";
import FormField from "./FormField.vue";
export default {
  components: {
    FormField
  },
  inheritAttrs: false,
  props: {
    value: {
      type: String,
      required: true
    },
    options: {
      type: Array,
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
    updateValue(value) {
      this.$emit("input", value);
    }
  }
};
</script>
<style>
.c-form-select {
  display: block;
  font-size: 16px;
}
</style>
