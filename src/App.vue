<template>
  <section class="container">
    <user-data
      :first-name="firstName"
      :last-name="lastName"
      :age="age"
    ></user-data>
    <button @click="setAge">Change Age</button>
    <div>
      <input type="text" placeholder="First Time" v-model="firstName" />
      <input type="text" placeholder="Last Time" ref="lastNameInput" />
      <button @click="setLastName">Set Name</button>
    </div>
  </section>
</template>

<script>
import { ref, computed, watch, provide } from 'vue';
import UserData from './components/UserData.vue';

export default {
  components: {
    UserData,
  },
  setup() {
    // const uName = ref('Abram');
    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null);
    const uAge = ref(25);

    // const user = reactive({
    //   name: 'Abram',
    //   age: 25,
    // });

    provide('userAge', uAge);

    const uName = computed(function () {
      return firstName.value + ' ' + lastName.value;
    });

    watch([uAge, uName], function (newValues, oldValues) {
      console.log('old age: ', oldValues[0]);
      console.log('new age: ', newValues[0]);
      console.log('old name: ', oldValues[1]);
      console.log('new name: ', newValues[1]);
    });

    function setNewAge() {
      uAge.value = 26;
    }

    // function setFirstName(event) {
    //   firstName.value = event.target.value;
    // }

    // function setLastName(event) {
    //   lastName.value = event.target.value;
    // }

    function setLastName() {
      lastName.value = lastNameInput.value.value;
    }

    return {
      userName: uName,
      age: uAge,
      setAge: setNewAge,
      firstName,
      lastName,
      lastNameInput,
      setLastName,
    };
  },
  // data() {
  //   return {
  //     userName: 'Maximilian',
  //   };
  // },
  // provide() {
  //   return { age: this.age }
  // }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>
