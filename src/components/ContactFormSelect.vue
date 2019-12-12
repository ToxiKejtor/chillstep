<template>
  <div>
    <label :for="id">{{ name }}</label>
    <select
      :id="id"
      class="c-contact-form-select"
      :name="name"
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
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      required: true
    },
    options: {
      type: Array,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      input: ""
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
.c-contact-form-select {
  display: block;
}
</style>
