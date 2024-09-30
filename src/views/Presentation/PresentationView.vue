<!-- <script setup>
import { onMounted, onUnmounted } from "vue";
import { RouterLink } from "vue-router";



//example components
import NavbarDefault from "../../examples/navbars/NavbarDefault.vue";
import DefaultFooter from "../../examples/footers/FooterDefault.vue";
import Header from "../../examples/Header.vue";
import DefaultCounterCard from "../../examples/cards/counterCards/DefaultCounterCard.vue";


//Vue Material Kit 2 components
import MaterialButton from "@/components/MaterialButton.vue";
import MaterialSocialButton from "@/components/MaterialSocialButton.vue";

// sections
import AuthorProfile from "/src/views/LandingPages/Author/Sections/AuthorProfile.vue";
import PresentationInformation from "./Sections/PresentationInformation.vue";
import AuthorPosts from "../LandingPages/Author/Sections/AuthorPosts.vue";

//images

import logoBootstrap from "@/assets/img/logos/bootstrap5.jpg";
import logoTailwind from "@/assets/img/logos/icon-tailwind.jpg";
import logoVue from "@/assets/img/logos/vue.jpg";
import logoAngular from "@/assets/img/logos/angular.jpg";
import logoReact from "@/assets/img/logos/react.jpg";
import logoSketch from "@/assets/img/logos/sketch.jpg";




const body = document.getElementsByTagName("body")[0];
onMounted(() => {
  body.classList.add("presentation");
  body.classList.add("bg-gray-200");
});
onUnmounted(() => {
  body.classList.remove("presentation");
  body.classList.remove("bg-gray-200");
});



</script>

<template>
  <div class="container position-sticky z-index-sticky top-0">
    <div class="row">
      <div class="col-10 ">
        <NavbarDefault :sticky="true" />
      </div>
    </div>
  </div>
  <Header>
    <div
    class="page-header min-vh-95"
    :style="{
      backgroundImage: 'url(./src/assets/img/HeaderInicio.png)',
      backgroundSize: 'cover',
      backgroundPosition: 'center',
      backgroundRepeat: 'no-repeat',
    }"
    loading="lazy"
  >
    <span class="mask bg-gradient-dark opacity-5"></span>
      <div class="container">
    <div class="row d-flex justify-content-end mx-auto " style="margin-top: -200px;">
      <div class="col-lg-8 text-end" >
            <h2
              class="text pt-12 "
              :style="{ color: '#840705'  }"
            >
            Parkinson Disease Assessment via Telemonitoring and Intelligence Technology Outcomes.
            </h2>
            <div class="text-sm mb-0 py-0 align-items-center d-flex justify-content-end">
              <samp class="mr-2 text-end"
              :style="{ color: 'white'  }"> Total de personas que forman parte del registro:     </samp>
            <DefaultCounterCard
            color="light"
            class="ml-3 small-counter-card"
            :count="10"
            suffix="+"
            :duration="3000"
            divider="vertical"
            style="width: 80px; height: 80px; font-size: 2px;"
            />
          </div>
        </div>
        <RouterLink to="/pages/landing-pages/Registro"> 
          <div class="row d-flex justify-content-end mt-3 me-2">
          <MaterialButton variant="gradient" color="primary" class="w-auto mt-1">
            Registrarse
          </MaterialButton>
        </div>
        </RouterLink>
        </div>
        </div>
    </div>
  </Header>
  
  <div class="card card-body blur shadow-blur mx-2 mx-md-4 mt-n6 mb-8">
    <AuthorProfile/>
    <div class="container">
  <div class="row">
  <section class="py-0 pb-6 " id="count-stats">
      <div class="d-flex justify-content-center text-center">
        <div class="col-md-3 position-relative">
          <DefaultCounterCard
            color="dark"
            title="ESTADOS"
            description="Total de estados que forman parte:"
            :count="10"
            suffix="+"
            :duration="3000"
            divider="vertical" 
          />
        </div>
        <div class="col-md-3">
          <DefaultCounterCard
           color="dark"
            title="REGISTROS"
            description="Total de registros actuales:"
            :count="1200"
            suffix="+"
            :duration="3000"
            divider="vertical" 
          />
        </div>
      </div>
  </section>
</div>
</div>
    <PresentationInformation />
    <AuthorPosts />
    <inline>
    <div class="container">
    <div class="row">
      <div class="d-flex flex-column w-100 text-center p-6 mb-4">
        <h3>Patrocinadores</h3>
    <div class="carousel">
          <div class="carousel-inner">
            <img v-for="(logo, index) in logos" :key="index" :src="logo" class="carousel-image" />
          </div>
       
        </div>
      </div>
    </div>
    </div>
  </inline>
    <div class="py-4">
      <div class="container">
        <div class="row">
          <div class="text-center mt-3 ms-auto">
            <h4 class="mb-0">¡Gracias por tú registro!</h4>
            <p class="lead mb-0">Siguenos</p>
          </div>
          <div class="text-center mt-4">
            <MaterialSocialButton
              route=""
              component="twitter"
              color="twitter"
              label="Tweet"
            />
            <MaterialSocialButton
              route=""
              component="facebook-square"
              color="facebook"
              label="Share"
            />
            <MaterialSocialButton
              route=""
              component="pinterest"
              color="pinterest"
              label="Pin it"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
  <DefaultFooter />
</template>

<script>
export default {
  data() {
    return {
      currentIndex: 0,
      logos: [
        logoBootstrap,
        logoTailwind,
        logoVue,
        logoAngular,
        logoReact,
        logoSketch
      ],
    };
  },
  methods: {
    goToSlide(index) {
      this.currentIndex = index;
    },
  },
};
</script>

<style scoped>
.carousel {
  position: relative;
  overflow: hidden;
}

.carousel-inner {
  display: flex;
  width: 100%; /* 100% * número de logos */
  animation: slide 12s infinite; /* Ajusta el tiempo total de la animación */
}

.carousel-image {
  width: 16.66%; /* 100 / número de logos */
  height: auto;
}

@keyframes slide {
  0% {
    transform: translateX(0);
  }
  16.66% {
    transform: translateX(-16.66%);
  }
  33.33% {
    transform: translateX(-33.33%);
  }
  50% {
    transform: translateX(-50%);
  }
  66.66% {
    transform: translateX(-33.33%);
  }
  83.33% {
    transform: translateX(-16.66%);
  }
  100% {
    transform: translateX(0);
  }
}
.small-counter-card {
  width:2px; 
  height: 2px;
  font-size: 8px;
}
</style> -->