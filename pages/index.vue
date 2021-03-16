<template>
<section>
  <header>
    <h1>Olicom</h1>
  </header>
  <main class="container">
    <Table v-if="usersList" :config="configList" :dataTable="usersList"/>
  </main>
</section>
</template>

<script>
import Table from "@/components/Table.vue"

export default {
  components: {
    Table
  },
  data() {
    return {
      usersList: null,
      configList: [
        {
          propKey: "name",
          name: "Imię i nazwisko",
        },
        {
          propKey: 'email',
          name: "E-mail",
        },
        {
          dataKey: 'company',
          propKey: 'name',
          name: "Nazwa firmy",
        },
        {
          dataKey: 'address',
          propKey: "city",
          name: "Miasto",
        },
        {
          propKey: "website",
          name: "Strona internetowa",
        }
      ]
    }
  },
  async mounted() {
    const users = await this.$axios.$get("https://jsonplaceholder.typicode.com/users")
    this.usersList = users
    console.log(users)
  }
}
</script>

<style lang="scss">
header {
  background: $navy-light;
  padding: 20px 0;
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
  h1 {
    color: $white;
  }
}
</style>
