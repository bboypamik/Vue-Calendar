<template>
    <div class="calendar container">
        <h1>Calendar</h1>
        <div  class="pt-5  calendar__top-bar">
            <p class="d-inline-flex font-weight-bold" v-for="day in state.days" :key="day">{{day}}</p>
        </div>
        <div class="calendar__numbers">
            <p class="d-inline-flex" v-for="num in 30" :key="num">{{num}}</p>
        </div>

        <button class="btn btn-primary"> Prev</button>
        <button class="btn btn-primary m-2">Next</button>
</div>
</template>

<script>
    import {reactive} from 'vue';
    export default {
        name: "calendar",

        setup(){

            const state = reactive({

                days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]

            })

            return {
                state
            }
        }
    }
</script>

<style scoped>

    .calendar__top-bar p {
        width: 14.28%;
    }

    .calendar__numbers p {
        width: 14.28%;
    }

</style>
