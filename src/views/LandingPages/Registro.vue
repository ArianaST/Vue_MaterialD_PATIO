<script setup>
import { onMounted, onUnmounted } from "vue";

//example components
import NavbarDefault from "../../examples/navbars/NavbarDefault.vue";
import DefaultFooter from "../../examples/footers/FooterDefault.vue";
import Formulario from "./Formulario.vue";
//Vue Material Kit 2 components
import MaterialAvatar from "@/components/MaterialAvatar.vue";


//image
import bg0 from "@/assets/img/HeaderInicio.png";
import profilePic from "@/assets/img/PATITO.png";
import MaterialButton from "@/components/MaterialButton.vue";
//dep
import Typed from "typed.js";


const body = document.getElementsByTagName("body")[0];
//hooks
onMounted(() => {
  body.classList.add("about-us");
  body.classList.add("bg-gray-200");
  
  onMounted(() => {
  setMaterialInput();
});

  if (document.getElementById("typed")) {
    // eslint-disable-next-line no-unused-vars
    var typed = new Typed("#typed", {
      stringsElement: "#typed-strings",
      typeSpeed: 90,
      backSpeed: 90,
      backDelay: 200,
      startDelay: 500,
      loop: true,
    });
  }
});
onUnmounted(() => {
  body.classList.remove("about-us");
  body.classList.remove("bg-gray-200");
});
</script>


 
<template>
   
  <div class="container position-sticky z-index-sticky top-0">
    <div class="row">
      <div class="col-12">
        <NavbarDefault :sticky="true" />
      </div>
    </div>
  </div>
  <header class="bg-gradient-dark">
    <div
      class="page-header min-vh-75"
      :style="{ backgroundImage: `url(${bg0})` }"
    >
      <span class="mask bg-gradient-dark opacity-6"></span>
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-lg-9 text-center mx-auto my-auto">
            <h1 class="text mb-0" 
            :style="{ color: '#840705'  }">
              Total de clientes que forman parte del registro <span class="text-white" id="typed"></span>
            </h1>
            <div id="typed-strings">
              <h1>team</h1>
              <h1>design</h1>
              <h1>tool</h1>
            </div>
            <p class="lead mb-4 py-2 text-white opacity-8">
              Total de registros actualmente +120  
            </p>

          </div>
        </div>
      </div>
    </div>
  </header>

  <div class="card card-body blur shadow-blur mx-2 mx-md-4 mt-n6 mb-8">
    <section class="py-sm-7 py-2 position-center">
  <div class="container">
  <div class="row">
    <div class="col-11 mx-auto">
          <div class="mt-n8 mt-md-n9 text-center">
            <div class="blur-shadow-logo">
              <MaterialAvatar
                size="xxl"
                class="shadow-xxl position-relative z-index-2"
                :image="profilePic"
                alt="Avatar"
              />
            </div>
          </div>
          <div class="row py-5">
            <div
              class="col-lg-8 col-md-7 z-index-2 position-relative px-md-2 px-sm-5 mx-auto"
            >
              <div
                class="d-flex justify-content-center align-items-center mb-2"
              >
              <h2 class="mb-2">¡Bienvenido al registro PATITO!</h2>

              </div>
              <p class="text-center mb-7"> Te invitamos a leer nuestro aviso de privavidad y carta consentimiento antes de ser aceptadas.</p>
              </div>
          <div>
    <Formulario/>
    <div class="row d-flex mx-auto py-3">
          <MaterialButton  variant="gradient" @onclick="Registrarse" color="primary" class="w-auto mt-1">
            Registrarse
          </MaterialButton>
        </div>
    <!-- <AboutTeam />
    <Featuring />
    <Newsletter /> -->
            </div>
          </div>
          </div>
    </div>
  </div>
</section>
</div>
  <DefaultFooter/>
</template>
 
<script>
export default {
  data() {
    return {
      isModalVisible: true, // Modal visible al iniciar
      showErrorAnimation: false, // Controla la animación de error
    };
  },
  methods: {
    closeModal() {
      // Aquí podrías poner alguna validación antes de cerrar
      this.isModalVisible = false;
    },
    handleClose() {
      // Disparar la animación si el modal es requerido
      this.showErrorAnimation = true;
      setTimeout(() => {
        this.showErrorAnimation = false; // Detener la animación después de cierto tiempo
      }, 100); // Duración de la animación
    },
  },
};
</script>

<style scoped>
.modal {
  display: none;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.modal.show {
  display: block;
  opacity: 1;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5); /* Fondo oscuro con opacidad */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1040;
}

.modal-dialog {
  z-index: 1050;
}
</style>