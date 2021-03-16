<template>
<div class="custom-table">
  <table>
    <input type="text" v-model="search" placeholder="Wyszukaj...">
      <thead>
        <tr>
          <th v-for="(item, id) in config" :key="id">
            {{ item.name }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, id) in computedTableData" :key="id">
          <td v-for="(item, id) in config" :key="id">
            <span v-if="item.propKey !== 'email'">
              {{ item.dataKey ? row[item.dataKey][item.propKey] : row[item.propKey]  }}
            </span>
            <a href="" v-if="item.propKey === 'email'">
              {{ item.dataKey ? row[item.dataKey][item.propKey] : row[item.propKey]  }}
            </a>
          </td>
        </tr>
      </tbody>
      <Pagination
        class="table-pagination"
        :totalRecords="searchTable.length"
        :perPageOptions="perPageOption"
        v-model="pagination"
      />
  </table>
</div>
</template>

<script>
import Pagination from "./pagination";

const perPageOption = 3;
export default {
  componnets: {
    Pagination
  },
  data() {
    return {
      perPageOption,
      pagination: {page: 1, perPage: perPageOption},
      search: '',
    }
  },
props: ["config", "dataTable"],
computed: {
    computedTableData: function() {
      if (!this.searchTable) return [];
      else {
        const firstIndex = (this.pagination.page - 1) * this.pagination.perPage;
        const lastIndex = this.pagination.page * this.pagination.perPage;
        return this.searchTable.slice(firstIndex, lastIndex);
      }
    },
    searchTable: function() {
      console.log(this.dataTable)
      const filter = new RegExp(this.search, "i")
      return this.dataTable.filter((el) => {
        return el.name.match(filter) || el.email.match(filter) || el.company.name.match(filter) || el.address.city.match(filter) || el.website.match(filter)
      })
    }
  }
}
</script>

<style lang="scss">
.custom-table {
  overflow-x: auto;
  table {
    width: 100%;
    background: $navy;
    padding: 45px 15px 45px 15px;
    border-radius: 5px;
    position: relative;
    input {
      position: absolute;
      top: 15px;
      right: 15px;
      background: #2f3341;
      border: 1px solid #343747;
      padding: 5px 10px;
      outline: none;
      width: 300px;
      border-radius: 4px;
      color: #9699a8;
      transition: .15s;
    }
    thead {
      tr {
        th {
          text-align: left;
          padding: 5px 10px 15px 10px;
        }
      }
    }
    tbody {
      tr {
        td {
          border-bottom: 1px solid #343747;
          padding: 10px 10px;
        }
        &:last-child {
          td {
            border-bottom: none;
          }
        }
      }
    }
    .table-pagination {
      position: absolute;
      bottom: 10px;
      right: 15px;
    }
  }
}

</style>