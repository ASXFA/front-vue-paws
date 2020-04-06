<template>
  <div class="home">
    <HeaderCora />
    <HeroCarousel />
    <WomenCarousel />
    <InstaCora />
    <PatnerLogo />
    <FooterCora />
  </div>
</template>

<script>
// @ is an alias to /src
import HeaderCora from "@/components/HeaderCora.vue";
import HeroCarousel from "@/components/HeroCarousel.vue";
import WomenCarousel from "@/components/WomenCarousel.vue";
import InstaCora from "@/components/InstaCora.vue";
import PatnerLogo from "@/components/PatnerLogo.vue";
import FooterCora from "@/components/FooterCora.vue";

export default {
  name: "Home",
  components: {
    HeaderCora,
    HeroCarousel,
    WomenCarousel,
    InstaCora,
    PatnerLogo,
    FooterCora,
  },
};
</script>
