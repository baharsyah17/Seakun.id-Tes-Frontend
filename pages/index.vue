<template>
  <div class="main-page">
    <div class="head-page">
      <logo />
    </div>
    <div class="mid-page">
      <div class="left-page">
        <Sidebar />
      </div>
      <div class="right-page">
        <Mainbar
          :data-akun="dataPage"
          :sortOption="sortOption"
          v-model="inputSearch"
          @search="search"
          @changeSorting="changeSorting"
        />
        <div class="page-box">
          <Pagnitation
            :page="page"
            :total="total"
            @previous="previous"
            @next="next"
            @getCurrentPage="getCurrentPage"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Logo from "../components/atoms/logo.vue";
import Sidebar from "../components/mollecules/sidebar.vue";
import Mainbar from "../components/mollecules/mainbar.vue";
import Pagnitation from "../components/atoms/pagnitation.vue";
export default {
  components: { Sidebar, Mainbar, Pagnitation, Logo },
  data() {
    return {
      dataAkun: [],
      dataPage: [],
      dataSearch: [],
      isDetailVisible: false,
      page: 1,
      limit: 5,
      total: 0,
      inputSearch: "",
      value: "",
      selectedOption: 1,
      sortOption: [
        {
          id: 1,
          name: "Sort",
        },
        {
          id: 2,
          name: "Ascending",
        },
        {
          id: 3,
          name: "Descending",
        },
      ],
    };
  },
  mounted() {
    this.getDataFromTes();
  },
  methods: {
    getDataFromTes() {
      var api = "https://demo3267455.mockable.io/order";
      axios
        .get(api)
        .then((res) => {
          this.dataSearch = res.data;
          this.dataAkun = res.data;
          this.getCurrentPage(this.page, this.limit);
          this.total = Math.ceil(this.dataAkun.length / this.limit);
        })
        .catch((err) => console.log(err));
    },
    getCurrentPage(page, limit = 5) {
      this.page = page;
      this.dataPage = [];
      const start = (page - 1) * limit;
      const end = page * limit;
      this.dataPage = this.dataAkun.slice(start, end);
    },
    previous() {
      this.page--;
      this.getCurrentPage(this.page, this.limit);
    },
    next() {
      this.page++;
      this.getCurrentPage(this.page, this.limit);
    },
    changeSorting(value) {
      this.selectedOption = value;
      if (this.selectedOption == 1) {
        this.getDataFromTes();
      }
      if (this.selectedOption == 2) {
        this.dataAkun.sort((a, b) => (a.createdAt > b.createdAt ? 1 : -1));
        this.getCurrentPage(this.page, this.limit);
      }
      if (this.selectedOption == 3) {
        this.dataAkun.sort((a, b) => (a.createdAt < b.createdAt ? 1 : -1));
        this.getCurrentPage(this.page, this.limit);
      }
    },
    search() {
      this.dataAkun = this.dataSearch;
      this.dataPage = [];
      const search = new RegExp(this.inputSearch, "i");
      this.dataAkun = this.dataAkun.filter(
        (d) => search.test(d.personalAccount.email) || search.test(d.orderId)
      );
      this.total = Math.ceil(this.dataAkun.length / this.limit);
      this.getCurrentPage(1, this.limit);
    },
  },
};
</script>

<style>
.main-page {
  position: relative;
}
.head-page {
  display: block;
  margin-top: 2px;
  margin-bottom: 2px;
  height: 60px;
  background-image: linear-gradient(135deg, #65fdf0 10%, #1d6fa3 100%);
}
.mid-page {
  display: flex;
}
.left-page {
  width: 17%;
  background-image: linear-gradient(135deg, #65fdf0 10%, #1d6fa3 100%);
}
.right-page {
  width: 83%;
  background-image: linear-gradient(135deg, #65fdf0 10%, #1d6fa3 100%);
}
</style>
