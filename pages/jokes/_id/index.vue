<template>
    <div>
        <nuxt-link to="/jokes">
            Back to Jokes
        </nuxt-link>
    <h2>{{joke.joke}}</h2>
    <hr/>
    <small>Joke ID: {{joke.id}}</small>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data () {
        return {
            joke: {}
        }
    },
    async created () {
        const config = {
            headers: {
                "Accept" : "application/json"
            }
        }
        try {
            const response = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config)
            this.joke = response.data
            
        } catch (error) {
            console.log(error)
        }
    },
    head () {
        return {
            title: this.joke.joke,
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
