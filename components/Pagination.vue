<template>
  <div class="custom-pagination">
    <i class="fas fa-chevron-left" @click="changePage(-1)"></i>
    <span>{{ page }} of {{ pages }}</span>
    <i class="fas fa-chevron-right" @click="changePage(1)"></i>
  </div>
</template>

<script>
export default {
  props: ["totalRecords", "perPageOptions"],
  data() {
    return {
      page: 1,
      perPage: this.perPageOptions
    };
  },
  computed: {
    pages() {
      const checker = this.totalRecords % this.perPage;
      if (checker > 0) {
        return Math.floor(this.totalRecords / this.perPage) + 1;
      } else {
        return this.totalRecords / this.perPage;
      }
    }
  },
  methods: {
    changePage(val) {
      switch (val) {
        case 0:
          this.page = 1;
          break;
        case -1:
          this.page = this.page > 1 ? this.page - 1 : this.page;
          break;
        case 1:
          this.page = this.page < this.pages ? this.page + 1 : this.page;
          break;
        case this.pages:
          this.page = this.pages;
          break;
      }

      this.$emit("input", { page: this.page, perPage: this.perPage });
    }
  }
};
</script>

<style lang="scss">
.custom-pagination {
  display: flex;
  align-items: center;
  span {
    margin: 0 10px;
  }
  i {
    font-size: 24px;
    cursor: pointer;
  }
}
</style>
