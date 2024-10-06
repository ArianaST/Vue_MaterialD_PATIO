<script setup>
import { ref, onMounted, onUnmounted } from "vue";


import NavbarDefault from "../../examples/navbars/NavbarDefault.vue";
import DefaultFooter from "../../examples/footers/FooterDefault.vue";
import MapaMexico from "./MapaMexico.vue";
import DatosRelevantes from "./DatosRelevantes.vue";


import bg0 from "@/assets/img/HeaderInicio.png";


import Typed from "typed.js";


const currentTab = ref('01');
const tabs = [
  { id: '01', name: 'Mapa interactivo' },
  { id: '02', name: 'Edades' },
  { id: '03', name: 'Sexo' },
  { id: '04', name: 'Frecuencia de metales y pesticidas' },
  { id: '05', name: 'Descargar los datos' },
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
        <!-- contenido para la pestaña de Edades -->
      </div>
      <div v-else-if="currentTab === '03'">
        <h2>Contenido para la pestaña de Sexo</h2>
        <!-- l contenido para la pestaña de Sexo -->
      </div>
      <div v-else-if="currentTab === '04'">
        <h2>Contenido para la pestaña de Frecuencia de metales y pesticidas</h2>
        <!--  contenido para la pestaña de Frecuencia de metales y pesticidas -->
      </div>
      <div v-else-if="currentTab === '05'">
        <h2>Aquí puedes descargar los datos del registro PATITO:</h2>
        <div class="logo-buttons-container">
    <!-- Botón 1 -->
    <div class="logo-button" @click="downloadExcel">
      <img src="@/assets/img/excel.png" alt="Logo Excel" class="logo-image">
      <span>Descargar Excel</span>
    </div>

    <!-- Botón 2 -->
    <div class="logo-button" @click="downloadJSON">
      <img src="@/assets/img/json.png" alt="Logo JSON" class="logo-image">
      <span>Descargar JSON</span>
    </div>
      </div>
    </div>
  </div>
  </div>
  <DefaultFooter />
</template>


<style scoped>

.tabs {
  display: flex;
  flex-wrap: wrap; 
  justify-content: center;
  margin-bottom: 30px;
}

.tabs button {
  padding: 12px 24px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
  margin: 10px 5px; 
  transition: background-color 0.3s ease, color 0.3s ease, transform 0.2s ease;
  border-radius: 8px; 
  font-size: 1rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); 
}

.tabs button.active {
  background-color: #840705;
  color: white;
  box-shadow: 0 6px 10px rgba(0, 0, 0, 0.15); 
}

@media (max-width: 768px) {
  .tabs button {
    font-size: 0.9rem; 
    padding: 10px 18px;
    width: 100%;
    text-align: center;
  }

  .tabs {
    flex-direction: column;
  }
}

@media (max-width: 576px) {
  .tabs button {
    font-size: 0.8rem; 
    padding: 8px 16px;
  }
}

.logo-buttons-container {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-top: 20px;
}

/*05 ESTILOS */
.logo-button {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: transparent;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
  width: 150px;
  text-align: center;
}

.logo-button:hover {
  transform: translateY(-5px); 
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15); 
}

.logo-image {
  width: 100px;
  height: 80px;
  margin-bottom: 10px;
  transition: transform 0.3s ease; 
}

.logo-button:hover .logo-image {
  transform: scale(1.1); 
}

.logo-button span {
  font-size: 1rem;
  font-weight: bold;
  color: #333;
}
</style>