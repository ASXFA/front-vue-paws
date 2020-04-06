<template>
  <div class="cart">
    <HeaderCora />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12 text-left">
            <div class="breadcrumb-text product-more">
              <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
              <span>Shopping Cart</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Shopping Cart Section Begin -->
    <section class="shopping-cart spad">
      <div class="container">
        <div class="row">
          <div class="col-lg-8">
            <div class="row">
              <div class="col-lg-12">
                <div class="cart-table">
                  <table>
                    <thead>
                      <tr>
                        <th>Image</th>
                        <th class="p-name text-center">Product Name</th>
                        <th>Price</th>
                        <th>Action</th>
                      </tr>
                    </thead>
                    <tbody v-if="userCart !== undefined && userCart.length > 0">
                      <tr v-for="(items, n) in userCart" :key="items.id">
                        <td class="cart-pic first-row">
                          <img :src="items.photo" />
                        </td>
                        <td class="cart-title first-row text-center">
                          <h5>{{ items.name }}</h5>
                        </td>
                        <td class="p-price first-row">${{ items.price }}</td>
                        <td class="delete-item">
                          <router-link to="/cart">
                            <a @click="removeCart(n)" href="#"
                              ><i class="material-icons">
                                close
                              </i></a
                            ></router-link
                          >
                        </td>
                      </tr>
                    </tbody>
                    <tbody v-else>
                      <tr>
                        <td colspan="4">
                          Your cart is Empty, Go buy some Products !
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
              <div class="col-lg-8 text-left">
                <h4 class="mb-4">
                  Informasi Pembeli:
                </h4>
                <div class="user-checkout">
                  <form>
                    <div class="form-group">
                      <label for="namaLengkap">Nama lengkap</label>
                      <input
                        type="text"
                        class="form-control"
                        id="namaLengkap"
                        aria-describedby="namaHelp"
                        placeholder="Masukan Nama"
                        v-model="customerInfo.name"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">Email Address</label>
                      <input
                        type="email"
                        class="form-control"
                        id="emailAddress"
                        aria-describedby="emailHelp"
                        placeholder="Masukan Email"
                        v-model="customerInfo.email"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">No. HP</label>
                      <input
                        type="text"
                        class="form-control"
                        id="noHP"
                        aria-describedby="noHPHelp"
                        placeholder="Masukan No. HP"
                        v-model="customerInfo.number"
                      />
                    </div>
                    <div class="form-group">
                      <label for="alamatLengkap">Alamat Lengkap</label>
                      <textarea
                        class="form-control"
                        id="alamatLengkap"
                        rows="3"
                        v-model="customerInfo.address"
                      ></textarea>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="row">
              <div class="col-lg-12 text-left">
                <div class="proceed-checkout">
                  <ul>
                    <li class="subtotal">
                      ID Transaction <span>#SH12000</span>
                    </li>
                    <li class="subtotal mt-3">
                      Subtotal <span>$ {{ totalHarga }}.00</span>
                    </li>
                    <li class="subtotal mt-3">
                      Pajak <span>10% = $ {{ pajak }}.00</span>
                    </li>
                    <li class="subtotal mt-3">
                      Total Biaya <span>$ {{ totalBiaya }}.00</span>
                    </li>
                    <li class="subtotal mt-3">
                      Bank Transfer <span>Mandiri</span>
                    </li>
                    <li class="subtotal mt-3">
                      No. Rekening <span>2208 1996 1403</span>
                    </li>
                    <li class="subtotal mt-3">
                      Nama Penerima <span>Shayna</span>
                    </li>
                  </ul>
                  <a @click="checkout()" href="#" class="proceed-btn">
                    <router-link to="/success"> ALREADY PAID</router-link></a
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Shopping Cart Section End -->
  </div>
</template>

<script>
import HeaderCora from "@/components/HeaderCora.vue";
import axios from "axios";

export default {
  name: "Cart",
  components: {
    HeaderCora,
  },
  data() {
    return {
      userCart: [],
      customerInfo: {
        name: "",
        email: "",
        number: "",
        address: "",
      },
    };
  },
  methods: {
    removeCart(id) {
      this.userCart.splice(id, 1);
      const parsed = JSON.stringify(this.userCart);
      localStorage.setItem("userCart", parsed);
      this.$forceUpdate();
    },
    checkout() {
      let productIds = this.userCart.map(function (product) {
        return product.id;
      });

      let checkoutData = {
        name: this.customerInfo.name,
        email: this.customerInfo.email,
        number: this.customerInfo.number,
        address: this.customerInfo.address,
        transaction_total: this.totalBiaya,
        transaction_status: "PENDING",
        transaction_details: productIds,
      };
      axios
        .post("http://127.0.0.1:8000/api/checkout", checkoutData)
        .then(() => this.$router.push("success"))
        // eslin-disable-next-lline no-console
        .catch((err) => console.log(err));
    },
  },
  computed: {
    totalHarga() {
      return this.userCart.reduce(function (items, data) {
        return items + data.price;
      }, 0);
    },
    pajak() {
      return (this.totalHarga * 10) / 100;
    },
    totalBiaya() {
      return this.totalHarga + this.pajak;
    },
  },
  mounted() {
    if (localStorage.getItem("userCart")) {
      try {
        this.userCart = JSON.parse(localStorage.getItem("userCart"));
      } catch (e) {
        localStorage.removeItem("userCart");
      }
    }
  },
};
</script>

<style lang="scss" scoped></style>
