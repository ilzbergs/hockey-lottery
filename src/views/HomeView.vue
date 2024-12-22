<template>
  <main>
    <TheWelcome />
  </main>
   <ul>
      <li v-for="(user, index) in users" :key="index">{{ user.name }}</li>
    </ul>
</template>
<script setup lang="ts">
import { ref, type Ref } from 'vue';
import TheWelcome from '../components/TheWelcome.vue'
</script>

 <script lang="ts">
interface User {
  name: string;
}

const users: Ref<User[]> = ref([]);
 const apiUrl = 'https://hockey-lottery-backend-2d87f1e6fb3c.herokuapp.com/api/users';

fetch(apiUrl)
  .then(response => response.json())
   .then(fetchedData => {
      users.value = fetchedData;  // Atjaunina data ref ar iegūtajiem datiem
      console.log('Users:', fetchedData);  // Attēlo datus konsolē
    })
  .catch(error => {
    console.error('Error fetching users:', error);
  });

</script>
