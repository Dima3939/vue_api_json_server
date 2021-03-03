<template>
  <div class="v-table">
    <div class="v-table_header">
      <p @click="sortByName">Name <i class="material-icons">unfold_more</i></p>
      <p @click="sortByPointsEarned">Points earned <i class="material-icons">unfold_more</i></p>
      <p @click="sortByPointsSpent">Points spent <i class="material-icons">unfold_more</i></p>
      <p @click="sortByDate">Registration date <i class="material-icons">unfold_more</i></p>
    </div>
    <div class="v-table__body">
      <v-table-row
      v-for="row in paginatedUsers"
      :key="row.id"
      :row_data="row"
      />
    </div>
    <div class="v-table-pagination">
      <div class="page" v-for="page in pages" :key="page" :class="{'page__selected': page === pageNumber}" @click="pageClick(page)">{{page}}</div>
    </div>
  </div>
</template>

<script>
  import vTableRow from './v-table-row'

  export default {
    name: "v-table",
    components: {
      vTableRow
    },
    props: {
      users_data: {
        type: Array,
        default: () => {
          return []
        }
      }
    },
    data() {
      return{
        usersPerPage: 20,
        pageNumber: 1
      }
    },
    computed: {
      pages() {
        return Math.ceil(this.users_data.length / 20);
      },
      paginatedUsers() {
        let from = (this.pageNumber - 1) * this.usersPerPage;
        let to = from + this.usersPerPage;
        return this.users_data.slice(from, to);
      }
    },
    methods: {
      pageClick(page) {
        this.pageNumber = page;
      },
      sortByName() {
        this.users_data.sort((a,b) => a.name.localeCompare(b.name))
      },
      sortByPointsEarned() {
        this.users_data.sort((a,b) => a.points_earned - b.points_earned)
      },
      sortByPointsSpent() {
        this.users_data.sort((a,b) => a.points_spent - b.points_spent)
      },
      sortByDate() {
        this.users_data.sort((a,b) => a.registration_date.localeCompare(b.registration_date))
      }
    }
  }
</script>

<style scoped>
.v-table {
  max-width: 900px;
  margin: 0 auto;
}
.v-table_header {
  display: flex;
  justify-content: space-around;
  border-bottom: solid 1px #42b983;
}
.v-table_header p {
  flex-basis: 25%;
  text-align: left;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.v-table-pagination {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 30px;
}
.page {
  padding: 8px;
  border: solid 1px #2c3e50;
  margin-right: 10px;
}
.page:hover {
  background: blueviolet;
  cursor: pointer;
  color: #ffffff;
}
.page__selected {
  background: blueviolet;
  cursor: pointer;
  color: #ffffff;
}
</style>