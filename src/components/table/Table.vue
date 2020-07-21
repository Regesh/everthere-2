<template>
    <table>
        <table-headers v-on:table-sorted="$emit('table-sorted', $event)"></table-headers>
        <table-row v-for="item in data" :key="item.uuid" v-bind:item='item'></table-row>
    </table>
</template>
<script>
import TableRow from './TableRow';
import TableHeaders from './TableHeaders';
export default {
    components: {
        TableRow,
        TableHeaders
    },
    props: {
        data: Array
    }
}
</script>

