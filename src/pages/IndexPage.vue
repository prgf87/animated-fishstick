<template>
  <q-page padding>
    <button
      class="btn"
      style="position: absolute; right: 20px"
      @click="counter++"
    >
      {{ counter }}
    </button>
    <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      ref="inputField"
    />

    <button @click="clearMessage">Clear Text</button>

    <h5 v-if="message.length" class="wrapper">{{ message }}</h5>

    <h6 v-else>No message written</h6>

    <hr />

    <p>Uppercase message: {{ uppercaseMessage }}</p>
    <p>Lowercase message: {{ lowercaseMessage(message) }}</p>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const inputField = ref(null);

const focusInput = () => {
  console.log('here');
  if (!inputField.value) {
    inputField.value.focus();
  }
};

onMounted(focusInput);

// export default {
//   data() {
//     return {
//       message: 'Learning Vue the hard way',
//       counter: 0,
//     };
//   },
//   computed: {
//     uppercaseMessage() {
//       console.log('messssss');
//       return this.message.toUpperCase() + ' ' + this.counter;
//     },
//   },
//   methods: {
//     clearMessage() {
//       this.message = '';
//     },
//     alertMessage() {
//       alert(this.message);
//     },
//     lowercaseMessage(value) {
//       return value.toLowerCase();
//     },

//   },
//   directives: {
//     autofocus: {
//       inserted(el) {
//         console.log('input inserted');
//         el.focus();
//       },
//     },
//   },
// };
</script>

<style>
.wrapper {
  border: 5px double slategray;
  padding: 10px;
}
.btn {
  padding-left: 20px;
  padding-right: 20px;
  padding-top: 5px;
  padding-bottom: 5px;
  background-color: slategray;
  border: 1px solid black;
  border-radius: 3px;
  color: white;
}
</style>
