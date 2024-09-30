<script setup>
import { RouterLink } from "vue-router";
import { ref, watch } from "vue";
import { useWindowsWidth } from "../../assets/js/useWindowsWidth";

import ArrDark from "@/assets/img/down-arrow-dark.svg";
import downArrow from "@/assets/img/down-arrow.svg";
import DownArrWhite from "@/assets/img/down-arrow-white.svg";

const props = defineProps({
  action: {
    type: Object,
    route: String,
    color: String,
    label: String,
    default: () => ({
      route: "https://www.creative-tim.com/product/vue-material-kit",
      color: "bg-gradient-success",
      label: "Free Download"
    })
  },
  transparent: {
    type: Boolean,
    default: false
  },
  light: {
    type: Boolean,
    default: false
  },
  dark: {
    type: Boolean,
    default: false
  },
  sticky: {
    type: Boolean,
    default: false
  },
  darkText: {
    type: Boolean,
    default: false
  }
});


// set text color
const getTextColor = () => {
  let color;
  if (props.transparent && textDark.value) {
    color = "text-dark";
  } else if (props.transparent) {
    color = "text-white";
  } else {
    color = "text-dark";
  }

  return color;
};


let textDark = ref(props.darkText);
const { type } = useWindowsWidth();

if (type.value === "mobile") {
  textDark.value = true;
} else if (type.value === "desktop" && textDark.value == false) {
  textDark.value = false;
}

watch(
  () => type.value,
  (newValue) => {
    if (newValue === "mobile") {
      textDark.value = true;
    } else {
      textDark.value = false;
    }
  }
);



</script>
<template>
  <nav
    class="navbar bg-white navbar-expand w-100 top-0" 
    
    :class="{
      ' z-index-3 w-100 shadow-none navbar-transparent position-absolute my-3':
        props.transparent,
      ' my-3 blur border-radius-lg z-index-3 py-2 shadow py-2 start-0 end-0 mx-4 position-absolute mt-4':
        props.sticky,
      'navbar-light bg-white py-3': props.light,
      'navbar-dark bg-gradient-dark z-index-3 py-3': props.dark,
      
    
    }"
  
  >
    <div
      :class="
        props.transparent || props.light || props.dark
          ? 'container'
          : 'container-fluid px-0 '"
    >
      <RouterLink
        class="navbar-brand d-none d-md-block"
        :style="{ color: '#840705' } "
        :class="[
          (props.transparent && textDark.value) || !props.transparent
            ? 'color text-center font-weight-bolder ms-sm-3'
            : 'text-dark font-weight-bolder ms-sm-3 mb-1'
        ]"
        :to="{name: 'presentation'}"
        rel="tooltip"
        title="PATITO"
        data-placement="bottom-image"
      >
      <img
                src="\src\assets\img\PATITO_sn.png"
                class="icon ms-sm-3 mb-1 mx-0"
                alt="icon"
                style="width: 30px; height: 30px"
              />
        PATITO
      </RouterLink>
      <RouterLink
        class="navbar-brand d-block d-md-none"
        :active-class="{ color: '#840705' } "
        :class="
          props.transparent || props.dark
            ? 'text-dark'
            : 'font-weight-bolder ms-sm-3'
        "
        to="/"
        rel="tooltip"
        title="PATITO"
        data-placement="bottom-image"
      >
        PATITO
      </RouterLink>
      
      <button
        class="navbar-toggler shadow-none ms-2"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navigation"
        aria-controls="navigation"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon mt-2">
          <span class="navbar-toggler-bar bar1"></span>
          <span class="navbar-toggler-bar bar2"></span>
          <span class="navbar-toggler-bar bar3"></span>
          <span class="navbar-toggler-bar bar4"></span>
          <span class="navbar-toggler-bar bar5"></span>
        </span>
      </button>

      <div
        class="collapse navbar-collapse w-100 pt-7 pb-8 py-lg-0"
        id="navigation"
      >
      <ul class=" navbar-nav navbar-nav-hover ms-auto">
      <li class="nav-item dropdown dropdown-hover mx-2">
        
      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-2 mt-0 ">
        <RouterLink to="/"
        >
          <i class="dropdown-header text-dark font-weight-bolder d-flex justify-content-center align-items-center p-0"
                :class="getTextColor()"
                ></i>
            Inicio

        </RouterLink>
      </div>
    </li>
      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-3 mt-0 "> 
        <RouterLink to="/pages/landing-pages/Registro" @click.prevent="showModal">
          <i class="dropdown-header text-dark font-weight-bolder d-flex justify-content-center align-items-center p-0"
                :class="getTextColor()"
                ></i>
                Registro
                
        </RouterLink>
        <Model :isModalVisible="isModalVisible" @update:isModalVisible="isModalVisible = $event"/>
      </div>

      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-3 mt-0 ">
        <RouterLink to="/pages/landing-pages/Datos">
                Datos
        </RouterLink>
      </div>
      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-3 mt-0 ">
        <RouterLink to="/pages/landing-pages/about-us">
          <i class="dropdown-header text-dark font-weight-bolder d-flex justify-content-center align-items-center p-0"
                :class="getTextColor()"
                ></i>
            Acerca de
            <img
                            :src="downArrow"
                            alt="down-arrow"
                            class="arrow  ms-auto"
                          />
        
        </RouterLink>
      </div>
      
      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-3 mt-0 ">
        <RouterLink to="/pages/landing-pages/contact-us">
          <i class="dropdown-header text-dark font-weight-bolder d-flex justify-content-center align-items-center p-0"
                :class="getTextColor()"
                ></i>
            Contacto
        </RouterLink>
      </div>
    </ul>        
      </div>
      </div>
      
  </nav>
  <!-- End Navbar -->
</template>
