<template>
    <div class="temperature">
        <input type="range" :min="min" :max="max"
        :value="value" 
        @input="handleInput" 
        :style="{backgroundColor: color}"
        class="temp"
        />
        <div class="labels">
            <div> {{ min }} </div>
            <div>temperature: {{ value }}F</div>
            <div>{{ max }}</div>
        </div>
        <div class="evaluation">{{ evaluation }}</div>
    </div>
</template>

<script>
export default {
    props: {
        cold: {
            type: Number,
            require: true,
        },
        hot: {
            type: Number,
            required: true,
        },
        max: {
            type: Number,
            default: 110,
        },
        min: {
            type: Number,
            default: 0
        },
        temperature: {
            type: Number,
            default: 0
        }
    },

    date() {
        return {
            value: this.temperature,
        };
    },

    computed: {
        color() {
            return this.evaluation === "cold"
                ? "blue"
                : this.evaluation === "hot"
                ? "red"
                : "green";
        },
        evaluation () {
            return this.value <= this.cold
                ? "cold"
                : this.value >= this.hot
                ? "hot"
                : "comfortable";
        },
    },

    methods: {
        handleInput(event) {
            this.value = Number(event.target.value);
            this.$emit("change", this.value);
        }
    }
}
</script>

<style scroped>
.evaluation {
    display: flex;
    font-weight: bold;
    justify-content: center;
}

input {
    appearance: none;
    background-color: gray;
    width: 100%;
}

.labels {
    display: flex;
    justify-content: space-between;
}

.temperature {
    width: 100%;
}
</style>