<template>
  <div class="app-container">
    <div class="filters">
      <filters></filters>
    </div>
    <div class="table-container">
      <Table v-on:table-sorted="sortLeadersData($event)" v-bind:data='filteredLeadersData'></Table>
    </div>
  </div>
</template>

<script>
import Table from "./components/table/Table";
import Filters from './components/filters/Filters';
export default {
  name: 'App',
  data: function() {
    return {
      leadersData: []
    }
  },
  components: {
    Table,
    Filters
  },
  methods: {
    sortLeadersData: function(sortObject) {
      if (sortObject.type === 'desc') {
        this.leadersData = this.leadersData.sort(function (a, b) {
          return a[sortObject.col] < b[sortObject.col] ? 1: -1;
        });
      } else {
        this.leadersData = this.leadersData.sort(function (a, b) {
          return a[sortObject.col] > b[sortObject.col] ? 1: -1;
        });
      }
    },
    fetchAssignmentData: function() {
      this.axios
      .get('./data/home_assignment_fe_tls_data.json')
      .then(res => res.data)
      .then(res => {
        this.leadersData = res;
      })
    }
  },
  mounted: function() {
    this.fetchAssignmentData();
  },
  computed: {
    filteredLeadersData: function() {
      return this.leadersData.slice(0, 8);
    }
  }
}
</script>