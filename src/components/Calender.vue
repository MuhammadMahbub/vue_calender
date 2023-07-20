<template>
    <div class="container">
        <section>
            <h1 class="text-center">Calender</h1>
            <h4>{{ currentMonth }} {{ currentYear }}</h4>{{ todayDate(date) }}
        </section>
    
        <section class="days d-flex">
            <p class="text-center" v-for="(day, index) in days" :key="index">{{ day }}</p>
        </section>

        <section class="dates">
            <p v-for="day in firstDay" :key="day"></p>
            <p :class="todayDate(date)" class="text-center" v-for="date in lastDate " :key="date">{{ date }}</p>
        </section>
        <section>
            <div class="d-flex justify-content-between">
                <button @click="prev" class="btn btn-dark">Prev</button>
                <button @click="next" class="btn btn-dark">Next</button>
            </div>
        </section>
    </div>
</template>

<script>
import { computed } from 'vue'
    export default {
        data() {
            return {
                days: ["Sun", 'Mon','Tue','Wed','Thu', 'Fri', 'Sat'],
                currentYear: new Date().getFullYear(),
                currMon: new Date().getMonth(),
            }
        },
        methods: {
            prev(){
                if(this.currMon === 0){
                    this.currentYear--
                    this.currMon = 11
                }else{
                    this.currMon--
                }
            },
            next(){
                if(this.currMon === 11){
                    this.currentYear++
                    this.currMon = 0
                }else{
                    this.currMon++
                }
            },
            todayDate(date){
               let allDate = new Date(this.currentYear,this.currMon,date).toDateString()
               let today = new Date().toDateString()
               return allDate == today ? "bg-danger" : ""
            }
        },
        computed: {
            currentMonth(){
                return new Date(this.currentYear, this.currMon).toLocaleString('default', { month: "long" })
            }, 
            firstDay() {
                return new Date(new Date().getFullYear(), this.currMon, 1).getDay();
            },
            lastDate() {
                return new Date(new Date().getFullYear(), this.currMon+1, 0).getDate();
            }
        },
        
    }
</script>

<style scoped>
.days p, .dates p{
    width: 14.28%;
}
.dates {
    display: flex;
    flex-wrap: wrap;
}
</style>