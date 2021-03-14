<template>
<div class="custom-table">
  <table>
      <thead>
        <tr>
          <th v-for="(item, id) in config" :key="id">
            {{ item.name }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, id) in dataTable" :key="id">
          <td v-for="(item, id) in config" :key="id">
            {{ item.dataKey ? row[item.dataKey][item.propKey] : row[item.propKey]  }}
          </td>
        </tr>
      </tbody>
  </table>
</div>
</template>

<script>
export default {
props: ["config", "dataTable"],
}
</script>

<style lang="scss">
.custom-table {
  overflow-x: auto;
  table {
    width: 100%;
    background: $navy;
    padding: 15px 15px 45px 15px;
    border-radius: 5px;
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
  }
}

</style>