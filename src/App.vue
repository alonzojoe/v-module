<script>
import { ref, onMounted, onBeforeMount, watch, watchEffect } from 'vue';
import Card from './components/Card.vue'

export default {
  components: {
    Card
  },
  setup() {

    const persons = ref([
      { id: 1, name: 'Alice', city: 'New York City', age: 28, color:'red' },
      { id: 2, name: 'Bob', city: 'Los Angeles', age: 35, color:'blue' },
      { id: 3, name: 'Charlie', city: 'Chicago City', age: 22, color:'green' },
      { id: 4, name: 'David', city: 'San Francisco', age: 42, color:'pink' },
      { id: 5, name: 'Eve', city: 'Miami', age: 30, color:'orange' },
    ])

    const filterUser = () => {
      persons.value = persons.value.filter((p) => p.age >= 30)
    }

    const deleteP = (id) => {

      let indexToRemove = persons.value.findIndex((p) => p.id == id)

      const confirmation = confirm("Are you sure?")

      if (confirmation) {
        if (indexToRemove !== -1) {
          persons.value.splice(indexToRemove, 1)
        }
      }

    }

    const filterCity = () => {
      const choosenCity = prompt("Filter: Enter City")

      persons.value = persons.value.filter((p) => p.city.toLowerCase().includes(choosenCity.toLocaleLowerCase()))

    }


    // onBeforeCreate(() => {
    //   console.log("onBeforeCreate hook: Component is about to be created.");
    // });

    // onCreated(() => {
    //   console.log("onCreated hook: Component has been created.");
    // });

    onBeforeMount(() => {
      console.log("onBeforeMount hook: Component is about to be mounted in the DOM.");
    });

    onMounted(() => {
      console.log("onMounted hook: Component has been mounted in the DOM.");
    });


    const numericData = ref(0)

    watch(numericData, (oldValue, newValue) => {
      if (oldValue === 3) {
        alert('You reached the limit');
      }
    })

    watchEffect(() => {
      numericData.value
      if (numericData.value == 4) {
         alert('this is watch effect')
      }
    })
    




    return {
      filterCity,
      filterUser,
      persons,
      deleteP,
      numericData
    }
  }
}

</script>

<template>
  <div>

    <button @click="numericData++">Increment: {{ numericData }}</button>
    <button @click="filterUser()">Filter By Age > 30</button>
    <button @click="filterCity()">Filter By City</button>

    <card v-for="(p, index) in persons" :key="p.id" :person="p" @delete-person="deleteP" />
    <p v-if="!persons.length">No record found</p>


  </div>
</template>

<style scoped></style>
