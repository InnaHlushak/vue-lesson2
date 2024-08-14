<template>
    <div class="container">
        <h3 >Вкажіть  дані</h3>
        <input type="text"  @input="name=$event.target.value" placeholder="Ім'я">
        <input type="text" v-model="email" placeholder="Емейл">
        <button v-if="name != '' " @click="showPfofile">Зберегти</button>
        <p class="error">{{error}} </p>
        <p>{{info}}</p>

    </div>
</template>

<script>
export default {
    data() {
        return  {
            name: "",
            email: "",
            error: "",
            info: ""
        }
    },
    methods: {
        showPfofile() {            
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (this.name.trim().length < 2  || !emailRegex.test(this.email)) {
                this.error = 'Дані вказано не коректно';
                return 
            }
            this.error = "";
            this.info = "Ваш профіль: "+ this.profile;
        }
    },
    computed: {
        profile() {
            if (this.name == "") return 
            return this.name + " , " + this.email
        }
    }  
}
</script>

<style scoped>
  .error {
    color: red;
  }
</style>
