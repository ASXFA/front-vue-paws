<template>
  <!-- Women Banner Section Begin -->
  <section class="women-banner spad">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12 mt-5" v-if="products.length > 0">
          <carousel
            class="product-slider"
            :nav="false"
            :dots="false"
            :autoplay="true"
          >
            <div class="product-item" v-for="items in products" :key="items.id">
              <div class="pi-pic">
                <img v-bind:src="items.galleries[0].photo" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view">
                    <router-link v-bind:to="'/product/' + items.id"
                      >+ Quick View</router-link
                    >
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">{{ items.type }}</div>
                <a href="#">
                  <h5>{{ items.name }}</h5>
                </a>
                <div class="product-price">
                  $14.00
                  <span>{{ items.price }}</span>
                </div>
              </div>
            </div>
          </carousel>
        </div>
        <div class="col lg-12" v-else>
          <p>
            Produk tidak tersedia !
          </p>
        </div>
      </div>
    </div>
  </section>
  <!-- Women Banner Section End -->
</template>

<script>
import carousel from "vue-owl-carousel";
import axios from "axios";

export default {
  name: "WomenCarousel",
  components: {
    carousel,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    axios
      .get("http://127.0.0.1:8000/api/products")
      .then((response) => (this.products = response.data.data.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style scoped>
.product-item {
  margin-right: 25px;
}
</style>
