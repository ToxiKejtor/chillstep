<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <ChillForm
      v-bind:title="formTitle"
      v-bind:description="formDescription"
      @formSent="this.handleFormSent"
    />
  </div>
</template>

<script>
import ChillForm from "./components/ChillForm.vue";

export default {
  name: "app",
  components: {
    ChillForm
  },
  data: function() {
    return {
      formTitle: 'Best "Contact Us" Ever',
      formDescription: "We would love to get in touch with you!"
    };
  },
  methods: {
    handleFormSent(sent) {
      const { title, description } = sent;
      this.formTitle = title;
      this.formDescription = description;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
