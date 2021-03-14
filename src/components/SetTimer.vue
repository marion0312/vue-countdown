<template>
    <div class="border">
        <h3>Timer Settings</h3>
        <form @submit.prevent="onSubmit($event)">
            <input type="text" v-model="timerName" placeholder="Timer Name">
            <input type="number" v-model="hour" placeholder="Hours">
            <input type="number" v-model="min" placeholder="Minutes">
            <input type="number" v-model="sec" placeholder="Seconds">
            <input type="submit" value="Set Timer">
        </form>
    </div>
</template>

<script>
import { validationMixin } from 'vuelidate'

export default {
    mixins: [validationMixin],
    name: "SetTimer",
    data() {
        return {
            hour: 0,
            min: 0,
            sec: 0
        }
    },
    methods: {
        onSubmit() {
            const timerSettings = {
                hour: this.hour,
                min: this.min,
                sec: this.sec,
                timerName: this.timerName
            }

            console.warn(timerSettings)


            this.$emit('set-timer', timerSettings);
            this.hour = ''
            this.min = ''
            this.sec = ''
            this.timerName = ''
        }
    },
    // validations: {
    //     hour: {required},
    //     min: {required},
    //     sec: {required}
    // }
}
</script>

<style scoped>
    .border {
        border: 1px solid black;
        border-radius: 5px;
    }

    form {
        display: flex;
    }

    input[type='number']
    {
        flex: 4;
        margin: 10px;
        padding: 10px;
    }

    input[type='text']
    {
        flex: 4;
        margin: 10px;
        padding: 10px;
    }

    input[type='submit']
    {
        flex: 4;
        margin: 10px;
        padding: 10px;

        background-color: lightseagreen;
        color: white;
        font-weight: bold;
        border: 1px solid lightseagreen;
        border-radius: 7px;

    }
</style>