<template>
    <div class="search-container">
        <input type='text' placeholder="search leader.." v-model="term" v-on:keyup="search()" />
    </div>
</template>
<script>
export default {
    methods: {
        search: function() {
            this.$emit('search', {term: this.term})
        }
    },
    data: function() {
        return {
            term: ''
        }
    }
}
</script>
<style scoped>
.search-container input {
    padding: 8px;
    border: 1px solid grey;
    border-radius: 25px;
    text-indent: 8px;
    outline: none;
}
</style>
