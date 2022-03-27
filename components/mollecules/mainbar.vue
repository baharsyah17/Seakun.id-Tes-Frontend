<template>
  <div class="mainbar-page">
    <div class="header">
      <h3>Order List</h3>
    </div>
    <div class="search-page">
      <div class="search-btn">
        <input
          class="search-input"
          type="text"
          v-model="inputVal"
          placeholder="Search By Name/Email/Order id"
        />
        <button class="search-button" @click="$emit('search')">Submit</button>
      </div>
      <div class="form-btn">
        <select
          class="sort"
          value="1"
          @change="$emit('changeSorting', $event.target.value)"
        >
          <option v-for="sort in sortOption" :key="sort.name" :value="sort.id">
            {{ sort.name }}
          </option>
        </select>
      </div>
    </div>
    <div class="data-list">
      <BoxData
        v-for="(dataAkun, id) in dataAkun"
        :key="id"
        :data-akun="dataAkun"
      />
    </div>
  </div>
</template>

<script>
import BoxData from "../atoms/box-data.vue";
export default {
  components: { BoxData },
  props: {
    dataAkun: {
      type: Array,
      default: () => [],
    },
    sortOption: {
      type: Array,
      default: () => [],
    },
    selectedOption: {
      type: Number,
      default: 1,
    },
    inputSearch: {
      type: String,
      default: "",
    },
  },
  computed: {
    inputVal: {
      get() {
        return this.inputSearch;
      },
      set(val) {
        this.$emit("input", val);
      },
    },
  },
};
</script>

<style>
.mainbar-page {
  padding-left: 15px;
  padding-right: 15px;
}
.header {
  position: flex;
  margin-bottom: 10px;
}
h3 {
  font-size: 40px;
}
.search-page {
  display: flex;
  justify-content: space-between;
}
.search-input {
  margin-top: 5px;
  padding-left: 10px;
  width: 350px;
  margin-right: 3px;
  border: 1px solid rgb(41, 206, 165);
  border-radius: 5px;
}
.search-button {
  background: rgb(41, 206, 165);
  color: white;
  border: 1px solid rgb(41, 206, 165);
  border-radius: 5px;
  padding-right: 10px;
  padding-left: 10px;
  cursor: pointer;
}
select {
  margin-top: 10px;
  border-color: rgb(41, 206, 165);
  border-radius: 5px;
  margin-right: 50px;
}
.search-btn {
  display: inline-block;
  line-height: 30px;
}
.form-btn {
  display: inline-block;
}
.data-list {
  margin-top: 20px;
}
</style>
