<template>
    <div class="calendar container">
        <h1>Calendar</h1>
        <div class="d-inline-flex">{{currentMonthName}} {{state.currentYear}}</div>
        <div  class="pt-5  calendar__top-bar">
            <p class="d-inline-flex font-weight-bold" v-for="day in state.days" :key="day">{{day}}</p>
        </div>
        <div class="calendar__numbers">
            <p class="d-inline-flex"  v-for="num in startDay" :key="num"> </p>
            <p class="d-inline-flex" v-for="num in daysInMonth()" :key="num"
            :class="currenDateClass(num)">{{num}} </p>
        </div>

        <button class="btn btn-primary" @click="prev()">Prev</button>
        <button class="btn btn-primary m-2" @click="next()">Next</button>
</div>
</template>

<script>
    import {reactive, computed} from 'vue';
    export default {
        name: "calendar",

        setup(){


            const state = reactive({

                currentDate: new Date().getUTCDate(),
                currentMonth: new Date().getMonth(),
                currentYear: new Date().getFullYear(),

                days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]

            })

           const currentMonthName = computed(() => {
                return new Date(
                    state.currentYear,
                    state.currentMonth
                ).toLocaleString("default", { month: "long" });
            },)

              const startDay = computed(() =>  new Date(state.currentYear, state.currentMonth, 1).getDay());

            function daysInMonth() {
                 return new Date(state.currentYear, state.currentMonth + 1, 0).getDate();
            }
            
            function prev() {
                if (state.currentMonth === 0) {
                    state.currentMonth = 11;
                    state.currentYear--;
                } else {
                    state.currentMonth--;
                }
            }

            function next() {
                if (state.currentMonth === 11){
                    state.currentMonth = 0;
                    state.currentYear++;
                }else {
                    state.currentMonth++;
                }

            }

           function currenDateClass(num) {
                const calenderFullDate = new Date(
                    state.currentYear,
                    state.currentMonth,
                    num
                ).toDateString();
                const currentFullDate = new Date().toDateString();
                return calenderFullDate === currentFullDate ? "text-danger " : "";
            }


            return {
                state,
                currentMonthName,
                startDay,
                daysInMonth,
                prev,
                next,
                currenDateClass
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

    .today {
        color: red;
    }

</style>
