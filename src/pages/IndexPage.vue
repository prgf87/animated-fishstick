<template>
  <q-page padding>
    <div>

      <div class="flex justify-around">
  
        <input
        v-model="message"
        @keyup.esc="clearMessage"
        @keyup.enter="alertMessage"
        v-autofocus
        ref="inputField"
        class="input"
        :class="{'error': message.length > 22}"
        />
        <!-- v-bind:class="{'error': message.length > 22}" -->
        <button
          class="btn ml-10"        
          @click="counter++"
          >
          {{ counter }}
        </button>
      </div>
  
      <button @click="clearMessage">Clear Text</button>
  
      <h3 v-if="message.length" class="wrapper">{{ message }}</h3>
  
      <h6 v-else class="wrapper">No message written</h6>
  
      <hr />
      <div class="space-y-4 py-8">
  
        <p>Uppercase message: {{ uppercaseMessage }}</p>
        <p>Lowercase message: {{ lowercaseMessage(message) }}</p>
      </div>
  
      <hr />
      <!-- v-bind: is the directive, but you can shorten it by just using the semicolon -->
      <div class="rug">
        <div class="grid mx-auto w-1/3">
          <img
            class="userPic"
            :class="gender"
            :src="picture"
            :alt="`${firstName} ${lastName}`"
          />
          <div class="flex justify-center items-center">
  
            <button :class="gender" class="btn1" v-on:click="getUser()">
              Generate Random User
            </button>
          </div>
        </div>
        <div class="grid mx-auto w-2/3">
          <h1>{{ firstName }} {{ lastName }}</h1>
          <h2>Email: {{ email }}</h2>
        </div>
      </div>
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
      gender: 'male',
      picture: 'https://randomuser.me/api/portraits/men/50.jpg',
    };
  },
  computed: {
    uppercaseMessage() {
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
    async getUser() {
      // console.log('hello');
      const res = await fetch('https://randomuser.me/api/', {
        method: 'GET',
      });
      console.log(res);
      const body = await res.json();
      const result = body.results[0];
      console.log(result);
      this.firstName = result.name.first;
      this.lastName = result.name.last;
      this.email = result.email;
      this.gender = result.gender;
      this.picture = result.picture.large;
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
  beforeCreate(){
    console.log('before create function')
  },
  created(){
    console.log('created function')
  },
  beforeMount(){
    console.log('beforeMount function')
  },
  mounted(){
    console.log('mounted function')
  },
  beforeUpdate(){
    console.log('before update function')  
  },  
  onUpdated(){
    console.log('update function');
  },
  beforeUnmount(){
    console.log('before destroyed function')
  },
  unmounted(){
    console.log('unmounted function')
  }
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
  font-size: 18px;

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
  font-size: 24px;
}

.wrapper {
  border: 5px double slategray;
  padding: 10px;
  background: yellow;
  width: 350px;
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
.btn1 {
  padding-left: 20px;
  padding-right: 20px;
  padding-top: 5px;
  padding-bottom: 5px;
  border-radius: 3px;
  width: 250px;
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

.col {
  display: grid;
  margin-left: calc(15%);
}

.error{
  color: red;
  background: pink;
}

button {
  cursor: pointer;
  display: inline-block;
  background: #333;
  color: white;
  border: 0;
  padding: 0.3rem 0.9rem;
}

button:focus {
  outline: none;
}

button:hover {
  transform: scale(1.02);
}

button:active {
  transform: scale(0.98);
}
</style>
