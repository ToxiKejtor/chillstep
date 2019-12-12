<template>
  <FormField :id="id" :label="label">
    <input
      :id="id"
      v-bind="$attrs"
      :type="type"
      :value="value"
      class="c-form-input"
      @change="updateValue"
    />
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
.c-form-input {
  display: block;
  width: 100%;
  font-size: 14px;
  padding: 5px;
}
</style>
