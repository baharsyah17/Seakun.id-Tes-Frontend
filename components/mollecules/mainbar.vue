<template>
  <div class="mainbar-page">
    <div class="header">
      <h3>Order List</h3>
    </div>
    <div class="search-page">
      <div class="search-btn">
        <input
          required
          class="search-input"
          type="text"
          id="search-name"
          v-model="inputVal"
        />
        <label for="search-name" class="input-label">Name/Email/Order id</label>
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
.search-button {
  margin-left: 10px;
  background-image: linear-gradient(135deg, #90f7ec 10%, #32ccbc 100%);
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
  position: relative;
  display: flex;
}
.search-input {
  width: clamp(100px, 75%, 400px);
  padding: 10px;
  border: none;
  border-radius: 4px;
  font: inherit;
  color: black;
  caret-color: rgb(41, 206, 165);
  background-color: transparent;
  outline: 2px solid rgb(41, 206, 165);
}
.input-label {
  position: absolute;
  top: 0;
  left: 0;
  transform: translate(10px, 10px);
  transition: transform 0.25s;
}
.search-input:focus + .input-label,
.search-input:valid + .input-label {
  transform: translate(10px, -14px) scale(0.8);
  color: rgb(41, 206, 165);
  padding-inline: 5px;
  background-color: #65fdf0;
}
.search-input:is(:focus, :valid) {
  outline-color: rgb(41, 206, 165);
}
.form-btn {
  display: inline-block;
}
select {
  background-image: linear-gradient(135deg, #90f7ec 10%, #32ccbc 100%);
}
select option {
  background-image: linear-gradient(135deg, #90f7ec 10%, #32ccbc 100%);
}
.data-list {
  margin-top: 20px;
}
</style>
