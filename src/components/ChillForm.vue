<template>
  <section class="c-contact">
    <div class="c-contact__inner">
      <header class="c-contact__header">
        <h2 class="c-contact__title">{{ title }}</h2>
        <div class="c-contact__description">{{ description }}</div>
      </header>
      <div class="c-form-container" v-if="!submitted">
        <div class="c-form-loader" v-show="loading">
          <Loader />
        </div>
        <div class="c-form-errors" v-if="errors.length">
          <ul class="c-form-errors__ul">
            <li
              class="c-form-errors__li"
              v-for="(error, index) in errors"
              :key="index"
            >
              {{ error }}
            </li>
          </ul>
        </div>
        <form
          id="c-contact-form-1"
          class="c-form"
          :class="{ 'c-form--loading': loading }"
          @submit.prevent="validateForm"
        >
          <label>
            <input
              type="text"
              name="name"
              class="c-form__input c-form__input--name"
              v-model.trim.lazy="form.name"
              :placeholder="form.placeholders.name"
            />
          </label>
          <label>
            <input
              type="email"
              name="email"
              class="c-form__input c-form__input--name"
              v-model.trim.lazy="form.email"
              :placeholder="form.placeholders.email"
            />
          </label>
          <label>
            <input
              type="number"
              name="age"
              class="c-form__input c-form__input--age"
              v-model.lazy="form.age"
              :placeholder="form.placeholders.age"
            />
          </label>
          <label>
            {{ form.placeholders.reason }}
            <select
              class="c-form__select c-form__select--reason"
              v-model="form.reason"
            >
              <option
                v-for="(option, index) in form.reasonOptions"
                :key="index"
                :value="option.value"
              >
                {{ option.text }}
              </option>
            </select>
          </label>
          <button type="submit">Submit</button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
import Loader from "./Loader.vue";
export default {
  name: "ChillForm",
  components: {
    Loader
  },
  props: ["title", "description"],
  data: function() {
    return {
      errors: [],
      submitted: false,
      loading: false,
      form: {
        placeholders: {
          name: "Enter your name",
          age: "Your age",
          email: "Email",
          reason: "What you're interested in"
        },
        name: null,
        email: null,
        age: null,
        reason: "all-news",
        reasonOptions: [
          { text: "all news", value: "all-news" },
          { text: "new products", value: "products" },
          { text: "new blog articles", value: "articles" }
        ]
      }
    };
  },
  methods: {
    validateForm: async function() {
      this.errors = [];
      if (!this.form.name) this.errors.push("Name required");
      if (!this.form.age) this.errors.push("Age is required");
      if (!this.form.email || this.form.email.indexOf("@") === -1) {
        this.errors.push("Valid email address is required");
      }
      if (!this.form.reason)
        this.errors.push("Select what you're interested in");

      if (!this.errors.length) {
        this.loading = true;
        const success = await this.submitForm();
        if (success) this.submitted = true;
        this.loading = false;
      }
    },
    submitForm: async function() {
      await this.sleep(1500);
      return true;
    },
    sleep: async function(m) {
      return new Promise(r => setTimeout(r, m));
    }
  }
};
</script>

<style scoped>
.c-contact {
  width: 600px;
  max-width: 100%;
  margin: 0 auto;
}

.c-contact__header {
  margin-bottom: 50px;
}

.c-form-container {
  position: relative;
}
.c-form {
  width: 300px;
  max-width: 100%;
  margin: 0 auto;
}
.c-form--loading {
  opacity: 0.5;
  pointer-events: none;
}

.c-form-loader {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;
}

.c-form__input {
  display: block;
  width: 100%;
  margin-bottom: 10px;
}
.c-form-errors {
  color: #ff0000;
  margin-bottom: 20px;
}
</style>
