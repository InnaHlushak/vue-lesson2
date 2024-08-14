<template>
    <div class="container">
        <h3>Використання watcher, опрацювання відповіді від HTTP запиту, відправлення API запитів:</h3>
        <label for="inputDate">Date:</label>
        <input type="date" id="inputDate" v-model="date"/>
        <p>Встановлена дата: {{getDate}}</p>
        <button @click = "getItem()">Показати JSON</button>
        <p v-if="item != null">{{item}}</p>
    </div>  
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {                   
            date: null,
            item: null, 
        }
    },
    methods: {
        getItem() {
            const API_KEY = "4ZOCEAdAoacmoaJHdEnQeIMDwsxFYAR8V7qYMddQ";
            axios.get(`https://api.nasa.gov/planetary/apod?api_key=${API_KEY}&date=${this.date}&thumbs=True`)
            .then(res => (this.item = res))
        }
    },
    computed: {
        getDate() {
            let myDate = this.date;
            return myDate;
        }
    },
    watch: {
        //спостерігач
        date(newValue,oldValue) {
            console.log(newValue,oldValue);
        },
        //глибинний спостерігач
        "item": {                       
            handler(newValue, oldValue) {
                console.log(newValue,oldValue);
            },
            deep: true,
            immediate: true
        },
    }
}
 
</script>