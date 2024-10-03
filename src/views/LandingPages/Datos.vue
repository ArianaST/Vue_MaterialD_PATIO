<script setup>
import { ref, onMounted, onUnmounted } from "vue";

//example components
import NavbarDefault from "../../examples/navbars/NavbarDefault.vue";
import DefaultFooter from "../../examples/footers/FooterDefault.vue";
import MapaMexico from "./MapaMexico.vue";
import DatosRelevantes from "./DatosRelevantes.vue";

//image
import bg0 from "@/assets/img/HeaderInicio.png";
import profilePic from "@/assets/img/PATITO.png";

//dep
import Typed from "typed.js";

// Estado para los tabs
const currentTab = ref('01');
const tabs = [
  { id: '01', name: 'Mapa interactivo' },
  { id: '02', name: 'Edades' },
  { id: '03', name: 'Sexo' },
  { id: '04', name: 'Frecuencia de metales y pesticidas' },
];

// Función para cambiar de tab
const changeTab = (tabId) => {
  currentTab.value = tabId;
};

//hooks
onMounted(() => {
  const body = document.body;
  body.classList.add("about-us", "bg-gray-200");

  if (document.getElementById("typed")) {
    new Typed("#typed", {
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
  const body = document.body;
  body.classList.remove("about-us", "bg-gray-200");
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
      class="page-header min-vh-95"
      :style="{ backgroundImage: `url(${bg0})` }"
    >
      <span class="mask bg-gradient-dark opacity-6"></span>
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-lg-8 text-center mx-auto my-auto">
            <h1 class="text mb-0"
            :style="{ color: '#840705'  }">
              Total de pacientes que forman parte del registro <span class="text-white" id="typed"></span>
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

  <div class="card card-body shadow-xl mx-3 mx-md-4 mt-n6">
    <DatosRelevantes/>
    
    <!-- Tabs -->
    <div class="tabs mt-2">
      <button 
        v-for="tab in tabs" 
        :key="tab.id" 
        @click="changeTab(tab.id)"
        :class="{ active: currentTab === tab.id }"
      >
        {{ tab.name }}
      </button>
    </div>

    <!-- Tab content -->
    <div class="tab-content mt-2">
      <div v-if="currentTab === '01'">
        <MapaMexico/>
      </div>
      <div v-else-if="currentTab === '02'">
        <h2>Contenido para la pestaña de Edades</h2>
        <!-- Añade aquí el contenido para la pestaña de Edades -->
      </div>
      <div v-else-if="currentTab === '03'">
        <h2>Contenido para la pestaña de Sexo</h2>
        <!-- Añade aquí el contenido para la pestaña de Sexo -->
      </div>
      <div v-else-if="currentTab === '04'">
        <h2>Contenido para la pestaña de Frecuencia de metales y pesticidas</h2>
        <!-- Añade aquí el contenido para la pestaña de Frecuencia de metales y pesticidas -->
      </div>
    </div>
  </div>

  <DefaultFooter />
</template>

<style scoped>

.tabs {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
}

.tabs button {
  padding: 10px 20px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
  margin: 0 5px;
  transition: background-color 0.3s, color 0.3s;
}

.tabs button.active {
  background-color: #840705;
  color: white;
}
</style>