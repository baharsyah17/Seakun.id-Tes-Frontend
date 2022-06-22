<template>
  <div>
    <div class="container" @click="showDetail">
      <div class="head-box">
        <div class="order-box">Order Id: {{ dataAkun.orderId }}</div>
        <div class="created-box">
          Created At: {{ dateString(dataAkun.createdAt) }}
        </div>
      </div>
      <div class="data-box">
        <div class="left-data">
          <h5>Info Akun</h5>
          <div>{{ dataAkun.personalAccount.name }}</div>
          <div>{{ dataAkun.personalAccount.email }}</div>
          <div>{{ dataAkun.personalAccount.phonenumber }}</div>
        </div>
        <div class="right-data">
          <div class="list-data">
            <div>profider</div>
            <div>paket</div>
            <div>exp</div>
          </div>
          <div class="info-data">
            <div>: {{ dataAkun.provider }}</div>
            <div>: {{ dataAkun.packet }}</div>
            <div>: Exp {{ dateString(dataAkun.expired) }}</div>
          </div>
          <div class="price-data">Rp {{ dataAkun.payment.paymentTotal }}</div>
        </div>
      </div>
    </div>

    <div class="detail-box" v-show="isDetailVisible">
      <h6>Order Detail</h6>
      <div class="detail-container">
        <div class="head-box">
          <div class="order-box">Order Id: {{ dataAkun.orderId }}</div>
          <div class="created-box">
            Created At: {{ dateString(dataAkun.createdAt) }}
          </div>
        </div>
        <div class="data-box">
          <div class="left-data">
            <h5>Info Akun</h5>
            <div>{{ dataAkun.personalAccount.name }}</div>
            <div>{{ dataAkun.personalAccount.email }}</div>
            <div>{{ dataAkun.personalAccount.phonenumber }}</div>
          </div>
          <div class="right-data">
            <div class="list-data">
              <div>profider</div>
              <div>paket</div>
              <div>exp</div>
            </div>
            <div class="info-data">
              <div>: {{ dataAkun.provider }}</div>
              <div>: {{ dataAkun.packet }}</div>
              <div>: Exp {{ dateString(dataAkun.expired) }}</div>
            </div>
            <div class="price-data">Rp {{ dataAkun.payment.paymentTotal }}</div>
          </div>
        </div>
      </div>
      <div class="box-info">
        <div class="box-infoleft">
          <div>Voucer code</div>
          <div>Payment Status</div>
          <div>Payment Date</div>
          <div>Payment Bank</div>
        </div>
        <div class="box-inforight">
          <div>: {{ dataAkun.voucherCode }}</div>
          <div>: {{ dataAkun.payment.status }}</div>
          <div>: {{ dateString(dataAkun.payment.paymentDate) }}</div>
          <div>: {{ dataAkun.payment.bank }}</div>
        </div>
      </div>
      <div class="btn-closeDetail">
        <button type="button" class="btn-close" @click="closeDetail">
          Oke
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDetailVisible: false,
    };
  },
  props: {
    dataAkun: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    dateString(value) {
      const oldDate = value;
      const newDate = new Date(oldDate).toLocaleString("id-ID", {
        day: "numeric",
        month: "long",
        year: "numeric",
      });
      return newDate;
    },

    showDetail() {
      this.isDetailVisible = true;
    },
    closeDetail() {
      this.isDetailVisible = false;
    },
  },
};
</script>

<style>
.container {
  background-image: linear-gradient(135deg, #90f7ec 10%, #32ccbc 100%);
  border: 3px solid rgb(41, 206, 165);
  border-radius: 10px;
  cursor: pointer;
  padding: 5px;
  margin-bottom: 20px;
}
.container:hover {
  background-color: white;
}
.head-box {
  display: flex;
  border-bottom: 2px solid teal;
  justify-content: space-between;
  padding-left: 5px;
  padding-right: 5px;
  color: black;
  font-weight: bold;
}

.data-box {
  display: flex;
  padding: 5px;
}
.left-data {
  width: 37%;
  color: black;
  font-weight: bold;
}
.right-data {
  width: 63%;
  display: flex;
  justify-content: space-around;
  color: black;
  font-weight: bold;
}
h5 {
  color: teal;
  font-weight: bold;
}
.list-data {
  border-left: 2px solid teal;
  padding-left: 15px;
  margin-top: 0;
  padding-top: 10px;
  color: teal;
}
.info-data {
  width: 40%;
  padding-top: 10px;
  margin-left: -12%;
}
.price-data {
  padding-top: 33px;
  justify-content: center;
}

.detail-box {
  position: fixed;
  top: 25%;
  left: 20%;
  width: 65%;
  background-color: black;
  border: 3px solid rgb(41, 206, 165);
  border-radius: 10px;
  padding: 5px;
}
h6 {
  color: teal;
  margin-top: 10px;
  margin-left: 30px;
  font-size: 20px;
  font-weight: bold;
}
.detail-container {
  background-color: whitesmoke;
  border: 3px solid rgb(41, 206, 165);
  border-radius: 10px;
  padding: 20px;
  margin: 20px;
}
.box-info {
  display: flex;
  background-color: whitesmoke;
  border: 3px solid rgb(41, 206, 165);
  border-radius: 10px;
  padding: 20px;
  margin: 20px;
  font-weight: bold;
}
.box-infoleft {
  margin-right: 40px;
}
.btn-closeDetail {
  float: right;
  margin-right: 20px;
  margin-bottom: 10px;
  width: 50px;
  text-align: center;
  background: rgb(41, 206, 165);
  color: white;
  border: 1px solid rgb(41, 206, 165);
  border-radius: 5px;
  cursor: pointer;
}
</style>
