<script setup>
import { ref, onMounted, onUnmounted } from "vue";

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

const isModalVisible = ref(true);
const showErrorAnimation = ref(false);


const closeModal = () => {
  isModalVisible.value = false;
};



const handleClose = () => {
  showErrorAnimation.value = true;
  setTimeout(() => {
    showErrorAnimation.value = false;
  }, 80);
};

const body = document.getElementsByTagName("body")[0];
//hooks
onMounted(() => {
  body.classList.add("about-us");
  body.classList.add("bg-gray-200");

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

<div v-if="isModalVisible" class="modal show fade" style="display: block;" aria-hidden="true">
    <div class="modal-overlay"></div>
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Aviso de privacidad</h5>
          <MaterialButton
            color="none"
            class="btn-close"
            @click="handleClose"
            aria-label="Close">
          </MaterialButton>
        </div>
        <div class="modal-body"> 
          <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quia perferendis facere quis, aliquid deserunt quasi, optio id eos dignissimos esse totam dicta aspernatur asperiores debitis nam ex, assumenda quisquam. Odio?
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Omnis rem ducimus officiis pariatur, veritatis dolorem perspiciatis? Amet praesentium, quaerat laboriosam quam alias excepturi mollitia dolorum quidem quas temporibus ab quod.
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Itaque, temporibus? Est cupiditate eos dolor! Aperiam, ab? Voluptatum deleniti vitae repellat necessitatibus veritatis dolores tenetur temporibus sequi, minima molestias explicabo similique!
          </p>
          
        </div>
        <div class="modal-footer justify-content-end">
          <MaterialButton
            variant="gradient"
            color="primary"
            @click="closeModal">
            Acepto el aviso de privacidad
          </MaterialButton>
        </div>
      </div>
    </div>
  </div>
  <div class="container position-sticky z-index-sticky top-0">
    <div class="row">
      <div class="col-10">
        <NavbarDefault :sticky="true" />
      </div>
    </div>
  </div>
  <header class="bg-gradient-dark">
    <div
      class="page-header min-vh-95"
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
            </div>
          </div>
          </div>
    </div>
  </div>
</section>
</div>
  <DefaultFooter/>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  z-index: 1050;
}

.modal-dialog {
  background-color: white;
  border-radius: 5px;
  max-width: 600px;
  width: 100%;
  z-index: 1060;
  position: relative;
  margin: 0 auto;
  top: 10%;
}

.modal-content {
  padding: 20px;
  max-height: 80vh;
  overflow-y: auto;
}

.btn-close {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}
</style>