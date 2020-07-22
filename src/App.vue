<template>
  <div class="app-container">
    <filters v-on:filter-table="filtersObject = $event"></filters>
    <div class="table-container">
      <Table v-on:table-sorted="sortObject = $event" v-bind:data='filteredLeadersData'></Table>
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
      leadersData: [],
      originalData: [],
      filtersObject: {
        term: ''
      },
      sortObject: {
        type: 'asc',
        col: 'rank'
      }
    }
  },
  components: {
    Table,
    Filters
  },
  methods: {
    fetchAssignmentData: function() {
      this.axios
      .get('./assets/data/home_assignment_fe_tls_data.json')
      .then(res => res.data)
      .then(res => {
        this.leadersData = this.originalData = res;
      })
    },
    sortLeaders: function() {
      const { type, col } = this.sortObject;
      if (type === 'desc') {
        this.leadersData = this.leadersData.sort(function (a, b) {
          return a[col] < b[col] ? 1: -1;
        });
      } else {
        this.leadersData = this.leadersData.sort(function (a, b) {
          return a[col] > b[col] ? 1: -1;
        });
      }
    },
    filterLeaders: function() {
      const { term } = this.filtersObject;
      let filteredLeaders = this.originalData;
      if (term !== '') {
        const loweredTerm = term.toLowerCase();
        filteredLeaders = filteredLeaders.filter(leader => leader['name'].toLowerCase().indexOf(loweredTerm) > -1 ||
        leader['company_name'].toLowerCase().indexOf(loweredTerm) > -1 ||
        leader['job_title'].toLowerCase().indexOf(loweredTerm) > -1);
      }
      this.leadersData = filteredLeaders;
    }
  },
  mounted: function() {
    this.fetchAssignmentData();
  },
  computed: {
    filteredLeadersData: function() {
      this.filterLeaders();
      this.sortLeaders();
      return this.leadersData.slice(0, 8);
    }
  }
}
</script>