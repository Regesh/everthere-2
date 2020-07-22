<template>
    <div class="filters-container">
        <search v-on:search="$emit('filter-table', $event)"></search> 
        filters
    </div>
</template>
<script>
import Search from './Search';
export default {
    components: {
        Search
    }
}
</script>
<style scoped>
.filters-container {
    display: grid;
    grid-template-columns: repeat(2, auto);
}
</style>

