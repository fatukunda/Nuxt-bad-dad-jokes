<template>
    <div>
        <searchJokes v-on:searchText ="searchText" />
        <AppJoke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke"/> 
    </div>
</template>

<script>
import axios from 'axios'
import AppJoke from '../../components/AppJoke'
import SearchJokes from '../../components/SearchJokes'
export default {
    asyncData () {
        return {
            jokes: []
        }
    },
    components: {
        AppJoke,
        SearchJokes
    },
    methods: {
        async searchText (text) {
            const config = {
                headers: {
                    "Accept": "application/json"
                }
            }
            try {
                const response = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`,config)
                this.jokes = response.data.results
            } catch (error) {
                console.log(error)
            }
        }
    },
    async created () {
        const config = {
            headers: {
                "Accept" : "application/json"
            }
        }
        try {
            const response = await axios.get("https://icanhazdadjoke.com/search", config)
            this.jokes = response.data.results
            
        } catch (error) {
            console.log(error)
        }
    },
    head () {
        return {
            title: "Dad Jokes",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: "Best place for corny dad jokes"
                }
            ]
        }
    }
}
</script>

<style>

</style>
