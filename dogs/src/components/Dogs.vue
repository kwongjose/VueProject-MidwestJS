<template>
    <div class="dogs">
        <table v-if="dogs.length != 0">
            <tr>
                <th> name </th>
                <th> Actions </th>
            </tr>
            <tr v-for="dog in dogs" :key="dog.name">
                <td> {{ dog.name }} </td>
                <td> <button @click="removeDog(dog)">&#x1f5d1;</button> </td>
            </tr>
        </table>
        <div>
            <label>Name</label>
            <input type="text" v-model="name" @keypress.enter="addDog">
            <button @click="addDog(dog)">Add</button>
        </div>
    </div>
</template>

<script>
// const URL_STR = null;
const URL_STR = 'http://localhost:1919/dog';

function sortDogs(dogs) {
    dogs.sort((dogA, dogB) => dogA.name.localeCompare(dogB.name))
    return dogs;
}
export default {

    props: {
        dogies: {
            type: Array,
            required: true,
        }
    },
    data() {
        return {
            dogs: this.dogies,
            name: ""
        }
    },

    async mounted () {
        try {
            if (URL_STR) {
                const res = await fetch(URL_STR);
                if (!res.ok) throw new Error(res.statusText);
                this.dogs = sortDogs(await res.json());
            } else {
                this.dogs = [ { name: "kitten" }, { name: "cat" } ]
            }
        } catch (e) {
            // console.error('error getting dogs:', e.message);
        }
       // this.dogs = [ { name: "kitten" }, { name: "cat" } ]
    },

    methods: {

        /**
         * Adds a dog to both the local list and remote
         */
        async addDog() {
            // If a dog with that name is already present, do nothing.
            const exists = this.dogs.some(dog => dog.name === this.name);
            if (!exists) {
                if (URL_STR) {
                    const res = await fetch(URL_STR, {method: "POST", body: this.name });
                    const dog = await res.json(); 
                    this.dogs = sortDogs(this.dogs.concat(dog));  
                } else {
                    this.dogs = sortDogs(this.dogs.concat( { name: this.name } ));
                }

            } 
            this.name = "";
        },

        /**
         * Removes a dog from both remote list and local model
         */
        async removeDog (dog) {
            const index = this.dogs.findIndex((item) => item.id === dog.id);
            if (URL_STR) {
                await fetch(`${URL_STR}/${dog.id}`, { method: "DELETE"});
            }

            this.dogs.splice(index, 1);
        }
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