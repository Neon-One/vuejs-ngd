
<template>
  <form id="form" @submit.prevent="submit" @reset="onReset">
    <div>
      <label>name</label>
      <input v-model="name" data-cy="firstName"/>
    </div>

    <div>
      <label>email</label>
      <input v-model="email" data-cy="email"/>
    </div>

    <div>
      <label>message</label>
      <textarea v-model="message" data-cy="message"></textarea>
    </div>

    <button type="submit" data-cy="submit">submit</button>
    <button type="reset" data-cy="reset">reset</button>
  </form>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: "",
      email: "",
      message: "",
    };
  },
  computed: {
    formValid() {
      
      const { name, email, message } = this;
      return (
        name.length > 0 &&
        /(.+)@(.+){2,}.(.+){2,}/.test(email) &&
        message.length > 0
      );
    },
  },
  methods: {
    onReset() {
      this.name = "";
      this.email = "";
      this.message = "";
    },
    submit() {
      if (!this.formValid) {
        return;
      }
      if (!localStorage.getItem("messages")) {
        localStorage.setItem("messages", JSON.stringify([]));
      }
      const messages = JSON.parse(localStorage.getItem("messages"));
      const { name, email, message } = this;
      messages.push({
        name,
        email,
        message,
      });
      localStorage.setItem("messages", JSON.stringify(messages));
      this.name = "";
      this.email = "";
      this.message = "";
      console.log("your entry is in local storage")
    },
  },
};
</script>




// Define it as a custom element
customElements.define('donation-window', Donation);