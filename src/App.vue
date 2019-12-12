<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <ContactForm
      :title="formTitle"
      :description="formDescription"
      @formSent="handleFormSent"
    />
  </div>
</template>

<script>
import ContactForm from "./components/ContactForm.vue";

export default {
  name: "App",
  components: {
    ContactForm
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
