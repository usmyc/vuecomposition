<template>
  <div class="wrapper">
    <div v-for="person in persons" :key="person.Name" class="home">
      <h1>{{ person.Name }}</h1>
      <h2>{{ person.Age }}</h2>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from "vue";
export default {
  name: "HomeView",
  setup() {
    const persons = ref([]);

    const load = async () => {
      try {
        let response = await fetch(
          "http://localhost:3000/Persons"
        );
        if (!response.ok) {
          throw new Error("Something went wrong!");
        } else {
          let data = await response.json();
          persons.value = data;
        }
        
      } catch (error) {
        console.log(error);
      }
    };
    load();

    return {
      persons,
    };
    
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  justify-content: center;
  align-items: center;
}
.home {
  margin: 10px;
  background: crimson;
  color: white;
  padding: 10px;
  max-width: fit-content;
}
</style>
