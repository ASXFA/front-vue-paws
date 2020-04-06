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
                <div class="product-thumbs">
                  <carousel
                    class="product-thumbs-track ps-slider"
                    :dots="false"
                    :nav="false"
                    :autoplay="true"
                    :autoplayTimeout="3500"
                  >
                    <div
                      class="pt"
                      @click="changeImage(thumb[0])"
                      :class="thumb[0] == photoDefault ? 'active' : ''"
                    >
                      <img src="img/mickey1.jpg" alt="" />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(thumb[1])"
                      :class="thumb[1] == photoDefault ? 'active' : ''"
                    >
                      <img src="img/mickey2.jpg" alt="" />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(thumb[2])"
                      :class="thumb[2] == photoDefault ? 'active' : ''"
                    >
                      <img src="img/mickey3.jpg" alt="" />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(thumb[3])"
                      :class="thumb[3] == photoDefault ? 'active' : ''"
                    >
                      <img src="img/mickey4.jpg" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-justify">
                  <div class="pd-title">
                    <span>oranges</span>
                    <h3>Pure Pineapple</h3>
                  </div>
                  <div class="pd-desc">
                    <p>
                      Lorem ipsum dolor sit amet consectetur adipisicing elit.
                      Corporis, error officia. Rem aperiam laborum voluptatum
                      vel, pariatur modi hic provident eum iure natus quos non a
                      sequi, id accusantium! Autem.
                    </p>
                    <p>
                      Lorem ipsum dolor sit, amet consectetur adipisicing elit.
                      Quam possimus quisquam animi, commodi, nihil voluptate
                      nostrum neque architecto illo officiis doloremque et
                      corrupti cupiditate voluptatibus error illum. Commodi
                      expedita animi nulla aspernatur. Id asperiores blanditiis,
                      omnis repudiandae iste inventore cum, quam sint molestiae
                      accusamus voluptates ex tempora illum sit perspiciatis.
                      Nostrum dolor tenetur amet, illo natus magni veniam quia
                      sit nihil dolores. Commodi ratione distinctio harum
                      voluptatum velit facilis voluptas animi non laudantium, id
                      dolorem atque perferendis enim ducimus? A exercitationem
                      recusandae aliquam quod. Itaque inventore obcaecati, unde
                      quam impedit praesentium veritatis quis beatae ea atque
                      perferendis voluptates velit architecto?
                    </p>
                    <h4>$495.00</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/cart" class="primary-btn pd-cart"
                      >Add To Cart</router-link
                    >
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
      photoDefault: "img/mickey1.jpg",
      thumb: [
        "img/mickey1.jpg",
        "img/mickey2.jpg",
        "img/mickey3.jpg",
        "img/mickey4.jpg",
      ],
    };
  },
  methods: {
    changeImage(urlImage) {
      this.photoDefault = urlImage;
    },
  },
};
</script>

<style scoped>
.product-thumbs .pt {
  margin-right: 10px;
}
</style>
