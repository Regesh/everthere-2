<template>
    <tr>
        <td>{{item.rank}}</td>
        <td>{{item.name}}</td>
        <td>
            <a :href="item.linkedin_url">
                <img v-bind:src="'/assets/images/in.png'">
            </a>
        </td>
        <td>{{item.job_title}}</td>
        <td>{{item.company_name}}</td>
        <td>{{item.industry}}</td>
        <td>{{item.relevancy_score}}</td>
        <td>{{item.exposure_score}}</td>
        <td>{{item.label}}</td>
    </tr>
</template>
<script>
export default {
    props: {
        item: Object
    }
}
</script>
<style scoped>
img {
    width: 10px;
    height: 10px;
}
tr {
    height: 45px;
}
td {
    padding: 8px;
}
</style>

