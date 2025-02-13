<script setup>
import { ref, onMounted, computed, watch } from 'vue'

const todos = ref([]);
const name = ref('');

const input_content = ref('');
const input_category = ref(null);

const todos_asc = computed(() => todos.value.sort((a, b) => {
  return b.createdAt - a.createdAt;
}));

const addTodo = () => {} 

watch(name, (newVal) => {
  localStorage.setItem('name', newVal);
})

onMounted (() => {
  name.value = localStorage.getItem('name') || '';
})
</script>

<template>

  <main class="app">

    <section class="greeting">
      <h2 class="title">
        Geef je naam: <input type="text" placeholder="name here" v-model="name"/>
      
      </h2>
    </section>
    
    <section class="create-todo">
      <h3>Maak een takenlijst</h3>

      <form @submit.prevent="addTodo">
        <h4>Wat staat er op je takenlijst {{ name }} ?</h4>
        <input type="text" placeholder="bv. boodschappen doen" v-model="input_content" />
        
        <h4>Kies een categorie</h4>

        <div class="options">
          <label>
            <input
            type="radio" 
            name="category"
            value="business"
            v-model="input_category" />

            <span class="bubble business"></span>
            <div>Werk gerelateerd</div>
          </label>

          <label>
            <input
            type="radio" 
            name="category"
            value="business"
            v-model="input_category" />

            <span class="bubble personal"></span>
            <div>Persoonlijk</div>
          </label>

        </div>

        <input type="submit" value="Toevoegen taak">
      </form>
    </section>
  </main>

</template>


