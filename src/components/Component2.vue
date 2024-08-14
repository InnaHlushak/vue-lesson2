<template>
    <div class="container">
        <h3>Фільтрування масиву:</h3>
        <p>1 Спосіб: із використанням методу для фільтрації масиву</p>
        <button @click = "showArray(myMovies())">Показати вихідний масив масив</button>
        <p>{{movies}}</p>
        <button @click = "filterArray(myMovies(),'комедія')">Показати відфільтрований масив</button>
        <p>{{filteredMovies}}</p>
        <p>2 Спосіб: із використанням  computed property </p>
        <input type="text" v-model="categoryMovie" placeholder="Категорія">
        <p>Відфільтрований масив за категорією <b>{{ categoryMovie }} </b></p>
        <p>{{filteredMoviesByCategory}}</p>
        <div>
            <p> За категорією <b>{{ categoryMovie }} </b> можете переглянути наступні фільми:</p>
            <ul>
                <li v-for="item in titlesFilteredMoviesByCategory">
                {{item}}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            movies: [], 
            filteredMovies: [],
            categoryMovie: '',
        }
    },
    methods: {
        myMovies() {
            const arr = [
                { 
                    title: "Пробудження",
                    category: "фантастика"
                },
                { 
                    title: "Дуплекс",
                    category: "комедія"
                },
                { 
                    title: "Гравітація",
                    category: "фантастика"
                }
            ]
            return arr
        },
        showArray(arr) {
            if (this.movies.length != 0) return;
            for (let item of arr) {
                this.movies.push(
                    {
                        title: item.title,
                        category: item.category
                    }
                )
            }
        },
        filterArray(arr,category) {
            if (this.filteredMovies.length != 0) return;
            for (let item of arr) {
                if (item.category == category) {
                    this.filteredMovies.push(item);
                }
            }
        }
    },
    computed: {
        filteredMoviesByCategory() {
            let resArr = [];
            for (let item of this.movies) {
                if (item.category == this.categoryMovie) {
                    resArr.push(item);
                }
            }
            return resArr;
        },
        titlesFilteredMoviesByCategory() {
            let arr = [];
            for (let item of this.filteredMoviesByCategory) {
                arr.push(item.title);
            }
            return arr;
        }
    }
}
</script>
