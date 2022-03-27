<template>
  <div class="box-page">
    <div class="pagination">
      <a :class="page === 1 ? 'hidden' : ''" @click="goToPrevius">Previus</a>
      <a
        v-for="(item, id) in total"
        :key="id"
        :class="page === item ? 'active' : ''"
        @click="$emit('getCurrentPage', item)"
        >{{ item }}</a
      >
      <a :class="page === 5 ? 'hidden' : ''" @click="goToNext">Next</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    page: {
      type: Number,
      default: 1,
    },
    total: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    goToPrevius() {
      this.$emit("previous");
    },
    goToNext() {
      this.$emit("next");
    },
  },
};
</script>

<style>
.pagination {
  float: right;
  margin-right: 25px;
  padding: 10px 5px;
  border-radius: 10px;
}
.pagination a {
  background-color: white;
  border: 1px solid black;
  border-radius: 5px;
  padding: 2px 6px;
  color: teal;
  margin-left: 15px;
  margin-right: 15px;
  cursor: pointer;
}
.hidden {
  display: none;
}

.pagination a.active {
  background-color: rgb(85, 204, 182);
  color: white;
}

.pagination a:hover:not(.active) {
  background-color: rgb(85, 204, 182);
  color: white;
}
</style>
