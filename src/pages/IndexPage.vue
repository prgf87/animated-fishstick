<template>
  <q-page padding>
    <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
    />

    <button @click="clearMessage">Clear Text</button>

    <h5 v-if="message.length" class="wrapper">{{ message }}</h5>

    <h6 v-else>No message written</h6>

    <hr />

    <p>Uppercase message: {{ uppercaseMessage() }}</p>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      message: 'I am VueJS!',
    };
  },
  methods: {
    clearMessage() {
      this.message = '';
    },
    alertMessage() {
      alert(this.message);
    },
    uppercaseMessage() {
      return this.message.toUpperCase();
    },
  },
};
</script>

<style>
.wrapper {
  border: 5px double gray;
  padding: 10px;
}
</style>
