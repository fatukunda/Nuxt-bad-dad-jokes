<template>
    <form @submit.prevent="searchJoke">
        <input type="text" v-model="text" placeholder="Search Jokes ...">
        <input type="submit" value="Search Jokes">
    </form>
</template>

<script>
export default {
    name: "SearchJokes",
    data () {
        return {
            text: ""
        }
    },
    methods: {
        searchJoke () {
            this.$emit('searchText', this.text)
            this.text=''
        }
    }
}
</script>

<style>

</style>
