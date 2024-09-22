<script setup>
import { onMounted } from "vue";

//Vue Material Kit 2 components
import MaterialAvatar from "@/components/MaterialAvatar.vue";
import MaterialButton from "@/components/MaterialButton.vue";

// image
import profilePic from "@/assets/img/PATITO.png";



onMounted(() => {
  setMaterialInput();
});
</script>
<template>
  <section class="py-sm-7 py-2 position-center">
    <div class="container">
      <div class="row">
        <div class="col-13 mx-auto">
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
                <h2 class="mb-4">¿Qué es el proyecto PATITO?</h2>
              </div>
    
              <p class="text-lg mb-0">
                Los registros de pacientes son sistemas organizados diseñados para recopilar y almacenar datos con el fin de analizar información sobre una población específica o una condición de salud determinada. 
                <p class="text-lg py-3 mb-0"> 
                  En el contexto de la Enfermedad de Parkinson (EP), una enfermedad crónica y neurodegenerativa que afecta a un gran número de personas a nivel global, la información recopilada tiene como propósito aproximarse a la prevalencia de la enfermedad, identificar los rasgos característicos de la población afectada y determinar los factores demográficos, genéticos o ambientales que inciden en el riesgo de desarrollar EP.
                <br />

                <div class="row d-flex justify-content-center  mt-5 me-3 ">
          <MaterialButton variant="gradient" color="primary" class="mb-0 w-auto">
            Preguntas Frecuentes        
          </MaterialButton>
         </div>
                </p>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
