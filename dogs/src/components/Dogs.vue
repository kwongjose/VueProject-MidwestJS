<template>
    <div class="dogs">
        <table v-if="dogs.length != 0">
            <tr>
                <th> name </th>
            </tr>
            <tr v-for="dog in dogs" :key="dog.name">
                <td> {{ dog.name }} </td>
            </tr>
        </table>
        <div>
            <lable>Name</lable>
            <input type="text" v-model="name" @keypress.enter="addDog">
            <button @click="addDog">Add</button>
        </div>
    </div>
</template>

<script>
function sortDogs(dogs) {
    dogs.sort((dogA, dogB) => dogA.name.localeCompare(dogB.name))
    return dogs;
}
export default {
    data() {
        return {
            dogs: [],
            name: ""
        }
    },
    methods: {
        addDog() {
        // If a dog with that name is already present, do nothing.
        const exists = this.dogs.some(dog => dog.name === this.name);
        if (!exists) {
            this.dogs = sortDogs(this.dogs.concat({name: this.name}));  
        } 
        this.name = "";
        },
    }
};
</script>

<style scoped>
    button, input {
        border: solid gray 1px;
        border-radius: 4px;
        padding: 4px;
    }
    input {
        margin: 0 10px;
    }
    label {
        font-weight: bold;
    }
    table {
        border-collapse: collapse;
        margin-bottom: 10px;
    }
    td, th {
        border: solid gray 1px;
        padding: 5px;
    }
</style>