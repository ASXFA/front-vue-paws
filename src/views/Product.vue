<template>
  <div class="product">
    <HeaderCora />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more text-left">
              <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="photoDefault" alt="" />
                </div>
                <div
                  class="product-thumbs"
                  v-if="
                    productDetails.galleries !== undefined &&
                    productDetails.galleries.length > 0
                  "
                >
                  <carousel
                    class="product-thumbs-track ps-slider"
                    :dots="false"
                    :nav="false"
                    :autoplay="true"
                    :autoplayTimeout="3500"
                  >
                    <div
                      v-for="pic in productDetails.galleries"
                      :key="pic.id"
                      class="pt"
                      @click="changeImage(pic.photo)"
                      :class="pic.photo == photoDefault ? 'active' : ''"
                    >
                      <img :src="pic.photo" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-justify">
                  <div class="pd-title">
                    <span>{{ productDetails.type }}</span>
                    <h3>{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <p v-html="productDetails.description"></p>
                    <h4>$ {{ productDetails.price }}</h4>
                  </div>
                  <div class="quantity">
                    <!-- <router-link to="/cart" class="primary-btn pd-cart"
                      >Add To Cart</router-link
                    > -->
                    <router-link to="/cart">
                      <a
                        @click="
                          saveCart(
                            productDetails.id,
                            productDetails.name,
                            productDetails.price,
                            photoDefault
                          )
                        "
                        href="#"
                        class="primary-btn pd-cart"
                        >Add to Cart</a
                      >
                    </router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedCora />
    <FooterCora />
  </div>
</template>

<script>
// @ is an alias to /src
import HeaderCora from "@/components/HeaderCora.vue";
import RelatedCora from "@/components/RelatedCora.vue";
import FooterCora from "@/components/FooterCora.vue";
import carousel from "vue-owl-carousel";
import axios from "axios";

export default {
  name: "Product",
  components: {
    HeaderCora,
    RelatedCora,
    FooterCora,
    carousel,
  },
  data() {
    return {
      photoDefault: "",
      productDetails: [],
      userCart: [],
    };
  },
  methods: {
    changeImage(urlImage) {
      this.photoDefault = urlImage;
    },
    setDataPhoto(data) {
      // ganti value dari productDetails dengan data Daro API
      this.productDetails = data;
      // ganti photoDefault sesuai denga id yg didapat dari API
      this.photoDefault = data.galleries[0].photo;
    },
    saveCart(idProduct, nameProduct, priceProduct, photoProduct) {
      var productStore = {
        id: idProduct,
        name: nameProduct,
        price: priceProduct,
        photo: photoProduct,
      };
      this.userCart.push(productStore);
      const parsed = JSON.stringify(this.userCart);
      localStorage.setItem("userCart", parsed);
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
    axios
      .get("http://127.0.0.1:8000/api/products", {
        params: {
          id: this.$route.params.id,
        },
      })
      .then((response) => this.setDataPhoto(response.data.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style scoped>
.product-thumbs .pt {
  margin-right: 10px;
}
.product-big-img {
  width: 100%;
  height: 100%;
}
</style>
