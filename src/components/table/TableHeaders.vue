<template>
    <tr>
        <td v-for="(col, index) in columns" :key="index" @click="sortCol(col)">
            <div class="data-container">
                <span class="col-name">{{col.label}}</span>
                <i v-if='col.field === sortedCol' class="arrow" :class="[sortType, {'sorted': col.field === sortedCol}]"></i>
            </div>
        </td>
    </tr>
</template>
<script>
export default {
    methods: {
        sortCol: function(col) {
            if (this.isSortable(col)) {
                this.sortType = (this.sortedCol === col.field) ? ((this.sortType == 'desc') ? 'asc' : 'desc') : 'desc';
                this.sortedCol = col.field;
                this.$emit('table-sorted', {
                    type: this.sortType,
                    col: this.sortedCol
                });
            }
        },
        isSortable: function(col) {
            return (col.label !== 'Relevancy' && col.label !== 'Exposure' && col.label !== 'Profile');
        }
    },
    data: function() {
        return {
            sortedCol: 'rank',
            sortType: 'asc',
            columns: [{label: 'Rank', field: 'rank'}, {label: 'Name', field: 'name'}, {label: 'Profile', field: 'Profile'},
             {label: 'Title', field: 'job_title'}, {label: 'Company', field: 'company_name'}, {label: 'Industry', field: 'industry'},
              {label: 'Relevancy', field: 'Relevancy'}, {label: 'Exposure', field: 'Exposure'}, {label: 'Type', field: 'label'}]
            }
    }
}
</script>
<style scoped>
.data-container {
    position: relative;
    display: grid;
    align-items: center;
    grid-template-columns: auto 25px;
}
.col-name {
    color: #616161;
    cursor: pointer;
}
.arrow {
  position: absolute;
  right: 7px;
  border: solid black;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
}
.arrow.asc {
    transform: rotate(-135deg);
  -webkit-transform: rotate(-135deg);
}
.arrow.desc {
    transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
}
</style>


