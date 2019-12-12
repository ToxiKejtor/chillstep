<template>
  <section class="c-contact-form">
    <div class="c-contact-form__inner">
      <header class="c-contact-form__header">
        <h2 class="c-contact-form__title">{{ title }}</h2>
        <div class="c-contact-form__description">{{ description }}</div>
      </header>
      <div v-if="!submitted" class="c-contact-form-container">
        <div v-show="loading" class="c-contact-form-loading-state">
          <ContactFormLoader />
        </div>
        <div v-if="errors.length" class="c-contact-form-errors">
          <ul class="c-contact-form-errors__ul">
            <li
              v-for="error in errors"
              :key="error"
              class="c-contact-form-errors__li"
            >
              {{ error }}
            </li>
          </ul>
        </div>
        <form
          id="c-contact-form-1"
          class="c-contact-form__form"
          :class="{ 'c-contact-form--loading': loading }"
          @submit.prevent="submitForm"
        >
          <FormInput
            v-model.trim="form.name"
            name="name"
            :placeholder="placeholders.name"
            type="text"
            :required="true"
          />

          <FormInput
            v-model.trim="form.email"
            name="email"
            :placeholder="placeholders.email"
            type="email"
            :required="true"
          />
          <FormInput
            v-model.trim="form.age"
            name="age"
            :placeholder="placeholders.age"
            type="number"
            :required="true"
          />
          <FormSelect
            id="c-contact-form-select--age"
            v-model="form.reason"
            name="reason"
            :placeholder="placeholders.reason"
            :options="reasonOptions"
          />
          <button type="submit" value="Submit">Submit</button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
import ContactFormLoader from "./ContactFormLoader.vue";
import FormInput from "./FormInput.vue";
import FormSelect from "./FormSelect.vue";

const sleep = m => new Promise(r => setTimeout(r, m));

export default {
  components: {
    ContactFormLoader,
    FormInput,
    FormSelect
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
      email: "Your Email",
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
    async submitForm() {
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
        const success = await this.sendForm();
        if (success) {
          this.submitted = true;
          this.$emit("formSent", this.sent);
        }
        this.loading = false;
      }
    },

    async sendForm() {
      await sleep(1500);
      return true;
    }
  }
};
</script>

<style>
.c-contact-form {
  width: 600px;
  max-width: 100%;
  margin: 0 auto;
}

.c-contact-form__header {
  margin-bottom: 50px;
}

.c-contact-form-container {
  position: relative;
}
.c-contact-form__form {
  width: 300px;
  max-width: 100%;
  margin: 0 auto;
}
.c-contact-form--loading {
  opacity: 0.5;
  pointer-events: none;
}

.c-contact-form-loading-state {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;
}

.c-contact-form-errors {
  color: #ff0000;
  margin-bottom: 20px;
}
</style>
