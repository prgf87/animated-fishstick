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
      class="input"
    />

    <button @click="clearMessage">Clear Text</button>

    <h3 v-if="message.length" class="wrapper">{{ message }}</h3>

    <h6 v-else>No message written</h6>

    <hr />

    <p>Uppercase message: {{ uppercaseMessage }}</p>
    <p>Lowercase message: {{ lowercaseMessage(message) }}</p>

    <hr />
    <!-- v-bind: is the directive, but you can shorten it by just using the semicolon -->
    <div class="rug">
      <div>
        <h1>{{ firstName }} {{ lastName }}</h1>
        <h3>{{ counter }}</h3>
        <h2>Email: {{ email }}</h2>
      </div>
      <img class="userPic" :src="picture" :alt="`${firstName} ${lastName}`" />
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      message: 'Learning Vue the hard way',
      counter: 0,
      firstName: 'John',
      lastName: 'Doe',
      email: 'user@email.com',
      gender: 'Male',
      picture: 'https://thispersondoesnotexist.com/',
    };
  },
  computed: {
    uppercaseMessage() {
      console.log('messssss');
      return this.message.length + ' ' + this.message.toUpperCase();
    },
  },
  methods: {
    clearMessage() {
      this.message = '';
    },
    alertMessage() {
      alert(this.message);
    },
    lowercaseMessage(value) {
      return this.message.length + ' ' + value.toLowerCase();
    },
  },
  directives: {
    autofocus: {
      inserted(el) {
        console.log('input inserted');
        el.focus();
      },
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  font-family: Arial, Helvetica, sans-serif;
}

/* #app {
  width: 400px;
  height: 100vh;
  margin: auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
} */

h1,
h2,
h3 {
  /* margin-bottom: 1rem; */
  font-weight: normal;
  font-size: larger;
}

img {
  border-radius: 50%;
  border: 5px #333 solid;
  /* margin-bottom: 1rem; */
}

.male {
  border-color: steelblue;
  background-color: steelblue;
}

.female {
  border-color: pink;
  background-color: pink;
  color: #333;
}

.input {
  padding: 0.4rem 0.9rem;
}

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

.userPic {
  height: 175px;
  width: 175px;
  border-radius: 100%;
  margin: auto;
}

.rug {
  display: flex;
  justify-items: center;
  align-items: center;
}

button {
  cursor: pointer;
  display: inline-block;
  background: #333;
  color: white;
  font-size: 18px;
  border: 0;
  padding: 0.3rem 0.9rem;
}

button:focus {
  outline: none;
}

button:hover {
  transform: scale(1.02);
}
</style>
