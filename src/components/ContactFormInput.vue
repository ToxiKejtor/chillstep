<template>
  <div>
    <label :for="id">{{ name }}</label>
    <input
      :id="id"
      :type="type"
      :name="name"
      :placeholder="placeholder"
      :required="required"
      :value="value"
      class="c-contact-form-input"
      @change="updateValue($event.target.value)"
    />
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      Number,
      default: ""
    },
    type: {
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
    required: {
      type: Boolean,
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
.c-contact-form-input {
  display: block;
  width: 100%;
  margin-bottom: 10px;
}
</style>
