<template>
    <div>
        <p :class="{ 'bg-green': hasCityExtension == 'Yes' }">ID: {{ person.id }} Name: {{ person.name }} Age: {{ person.age
        }} City: {{ person.city }} <a href="" @click.prevent="deletePerson()">Delete</a></p>
    </div>
</template>

<script>
import { computed } from 'vue'
export default {
    props: {
        person: {
            type: Object,
            required: true,
            default: () => ({ id: 0, name: '', city: '', age: 0 })

        }
    },

    emits: ['delete-person'],

    setup(props, { emit }) {

        const deletePerson = () => {
            emit('delete-person', props.person.id)
        }

        const hasCityExtension = computed(() => {
            return props.person.city.toLowerCase().includes("city") ? 'Yes' : 'No'
        })

        return {
            deletePerson,
            hasCityExtension
        }
    }
}
</script>

<style scoped>
a {
    border: 1px solid #eee;
    border-radius: 15px;
    background: red;
    color: #fff;
    margin-left: 4px;
    padding: .3rem 1rem;
}

.bg-green {
    background-color: green;
}
</style>