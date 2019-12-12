<template>
  <div>
    <label :for="id">{{ name }}</label>
    <input
      :id="id"
      v-bind="$attrs"
      :type="type"
      :name="name"
      :value="value"
      class="c-contact-form-input"
      @change="updateValue"
    />
  </div>
</template>

<script>
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
    name: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      id: this.getRandomId(1, Math.pow(10, 8))
    };
  },
  methods: {
    updateValue(event) {
      this.$emit("input", event.target.value);
    },
    getRandomId(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
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
