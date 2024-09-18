<script setup>
import { onMounted } from "vue";

//Vue Material Kit 2 components
import MaterialAvatar from "@/components/MaterialAvatar.vue";
import MaterialButton from "@/components/MaterialButton.vue";

// image
import profilePic from "@/assets/img/bruce-mars.jpg";

// material-input
import setMaterialInput from "@/assets/js/material-input";
onMounted(() => {
  setMaterialInput();
});
</script>
<template>
  <section class="py-sm-7 py-5 position-relative">
    <div class="container">
      <div class="row">
        <div class="col-12 mx-auto">
          <div class="mt-n8 mt-md-n9 text-center">
          </div>
          <div class="row py-7">
            <div
              class="col-lg-7 col-md-7 z-index-2 position-relative px-md-2 px-sm-5 mx-auto"
            >
              <div
                class="d-flex justify-content-between align-items-center mb-2"
              >
                <h3 class="mb-0">Sobre Nosotos</h3>
                <h3 class="mb-0">¡Somos PATITO!</h3>
              </div>
              <p class="text-lg mb-0">
                Somos un resgistro mexicano que busca pacientes con la enfermedad de parkinson,PATITO tiene como 
                finalidad recolectar datos demograficos, medicos, ambientales, cognitivos y de estilo de vida para mejorar mediante
                estos datos la amplitud de la enfermedad de parkinson en la población mexicana... 
              </p>
              <div >
                <MaterialButton variant="gradient" color="primary" class="w-auto me-9">Aviso de privacidad</MaterialButton>
                <MaterialButton variant="gradient" color="primary" class="w-auto me-9">Carta de consentimiento</MaterialButton>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
