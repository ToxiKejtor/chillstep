<template>
  <section class="c-contact">
    <div class="c-contact__inner">
      <header class="c-contact__header">
        <h2 class="c-contact__title">{{ title }}</h2>
        <div class="c-contact__description">{{ description }}</div>
      </header>
      <div v-if="!submitted" class="c-form-container">
        <div v-show="loading" class="c-form-loader">
          <ContactFormLoader />
        </div>
        <div v-if="errors.length" class="c-form-errors">
          <ul class="c-form-errors__ul">
            <li
              v-for="(error, index) in errors"
              :key="index"
              class="c-form-errors__li"
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
              v-model.trim.lazy="form.name"
              type="text"
              name="name"
              class="c-form__input c-form__input--name"
              :placeholder="placeholders.name"
            />
          </label>

          <label>
            <input
              v-model.trim.lazy="form.email"
              type="email"
              name="email"
              class="c-form__input c-form__input--name"
              :placeholder="placeholders.email"
            />
          </label>

          <label>
            <input
              v-model.lazy="form.age"
              type="number"
              name="age"
              class="c-form__input c-form__input--age"
              :placeholder="placeholders.age"
            />
          </label>

          <label>
            {{ placeholders.reason }}
            <select
              v-model="form.reason"
              class="c-form__select c-form__select--reason"
              name="reason"
            >
              <option
                v-for="option in reasonOptions"
                :key="option.value"
                :value="option.value"
              >
                {{ option.text }}
              </option>
            </select>
          </label>
          <button type="submit" value="Submit">Submit</button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
import ContactFormLoader from "./ContactFormLoader.vue";

const sleep = m => new Promise(r => setTimeout(r, m));

export default {
  components: {
    ContactFormLoader
  },

  props: {
    title: {
      type: String,
      required: true
    },

    description: {
      type: String,
      default: ""
    }
  },

  data() {
    return {
      errors: [],
      submitted: false,
      loading: false,
      form: {
        name: null,
        email: null,
        age: null,
        reason: "all-news"
      }
    };
  },

  computed: {
    placeholders: () => ({
      name: "Enter your name",
      age: "Your age",
      email: "Email",
      reason: "What you're interested in"
    }),

    reasonOptions: () => [
      { text: "all news", value: "all-news" },
      { text: "new products", value: "products" },
      { text: "new blog articles", value: "articles" }
    ],

    sent: () => ({
      title: "Thanks for sending form!",
      description: "We will be in touch with you shortly!"
    })
  },

  methods: {
    async validateForm() {
      this.errors = [];
      if (!this.form.name) this.errors.push("Name required");
      if (!this.form.age) this.errors.push("Age is required");
      if (!this.form.email || !this.form.email.includes("@")) {
        this.errors.push("Valid email address is required");
      }
      if (!this.form.reason)
        this.errors.push("Select what you're interested in");

      if (!this.errors.length) {
        this.loading = true;
        const success = await this.submitForm();
        if (success) {
          this.submitted = true;
          this.$emit("formSent", this.sent);
        }
        this.loading = false;
      }
    },

    async submitForm() {
      await sleep(1500);
      return true;
    }
  }
};
</script>

<style>
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
