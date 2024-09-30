<template>
  <div class="ContainerTabs">
  

   
      <div class="mapa-container">
      <div class="mapa-svg" v-html="svgMapa" @click="resetSeleccion"></div>
      <div v-if="estadoSeleccionado" class="info-estado">
        <h2>{{ infoEstados[estadoSeleccionado]?.nombre }}</h2>
        <p>Capital: {{ infoEstados[estadoSeleccionado]?.capital }}</p>
        <p>Población: {{ infoEstados[estadoSeleccionado]?.poblacion }}</p>
      </div>
    </div>

    <!-- <div v-if="currentTab === '02'" class="tab-content">
      <div>
       <BarChart :chartData="chartData" :options="chartOptions" />
      </div>
    </div> -->

  </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  // import { Bar } from 'vue-chartjs'
  // import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
  // ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

  
  export default {
    // components: {
    // BarChart: Bar
    // },
    setup() {
      
      // mapa
      const svgMapa = ref('');
      const estadoSeleccionado = ref(null);
      const infoEstados = {
        MXSON: { nombre: "sonora", capital: "Redacted", poblacion: "redacted" },
        MXBCN: { nombre: "Baja California", capital: "Redacted", poblacion: "redacted" },
        MXCHH: { nombre: "Chihuahua", capital: "Redacted", poblacion: "redacted" },
        MXCOA: { nombre: "Coahuila", capital: "Redacted", poblacion: "redacted" },
        MXTAM: { nombre: "Tamaulipas", capital: "Redacted", poblacion: "redacted" },
        MXNLE: { nombre: "Nuevo leon", capital: "Redacted", poblacion: "redacted" },
        MXROO: { nombre: "Quintana Roo", capital: "Redacted", poblacion: "redacted" },
        MXCAM: { nombre: "Campeche", capital: "Redacted", poblacion: "redacted" },
        MXTAB: { nombre: "Tabasco", capital: "Redacted", poblacion: "redacted" },
        MXCHP: { nombre: "Chiapas", capital: "Redacted", poblacion: "redacted" },
        MXCOL: { nombre: "Colima", capital: "Redacted", poblacion: "redacted" },
        MXNAY: { nombre: "Nayarit", capital: "Redacted", poblacion: "redacted" },
        MXBCS: { nombre: "Baja California Sur", capital: "Redacted", poblacion: "redacted" },
        MXSIN: { nombre: "Sinaloa", capital: "Redacted", poblacion: "redacted" },
        MXYUC: { nombre: "Yucatan", capital: "Redacted", poblacion: "redacted" },
        MXVER: { nombre: "Veracruz", capital: "Redacted", poblacion: "redacted" },
        MXJAL: { nombre: "Jalisco", capital: "Redacted", poblacion: "redacted" },
        MXMIC: { nombre: "Michoacan", capital: "Redacted", poblacion: "redacted" },
        MXGRO: { nombre: "Guerrero", capital: "Redacted", poblacion: "redacted" },
        MXOAX: { nombre: "Oaxaca", capital: "Redacted", poblacion: "redacted" },
        MXMEX: { nombre: "Mexico", capital: "Redacted", poblacion: "redacted" },
        MXPUE: { nombre: "Puebla", capital: "Redacted", poblacion: "redacted" },
        MXMOR: { nombre: "Morelos", capital: "Redacted", poblacion: "redacted" },
        MXQUE: { nombre: "Queretaro", capital: "Redacted", poblacion: "redacted" },
        MXHID: { nombre: "Hidalgo", capital: "Redacted", poblacion: "redacted" },
        MXGUA: { nombre: "Guanajuato", capital: "Redacted", poblacion: "redacted" },
        MXSLP: { nombre: "San Luis Potosi", capital: "Redacted", poblacion: "redacted" },
        MXZAC: { nombre: "Zacatecas", capital: "Redacted", poblacion: "redacted" },
        MXAGU: { nombre: "Aguascalientes", capital: "Aguascalientes", poblacion: "1,425,607" },
        MXDUR: { nombre: "Durango", capital: "Durango", poblacion: "1,832,650" },
        MXTLA: { nombre: "Tlaxcala", capital: "Tlaxcala", poblacion: "1,342,977" },
        MXCMX: { nombre: "Ciudad de México", capital: "Ciudad de México", poblacion: "9,209,944" },
      };
  
      const cargarSVG = async () => {
        try {
          const response = await fetch('/mx.svg');
          svgMapa.value = await response.text();
        } catch (error) {
          console.error('Error al cargar el SVG:', error);
        }
      };
  
      const seleccionarEstado = (event) => {
        const estado = event.target.closest('path');
        if (estado) {
          estadoSeleccionado.value = estado.id;
        }
      };
  
      const resetSeleccion = () => {
        estadoSeleccionado.value = null;
      };
  
      onMounted(() => {
        cargarSVG();
        setTimeout(() => {
          const mapaContainer = document.querySelector('.mapa-svg');
          if (mapaContainer) {
            mapaContainer.addEventListener('click', seleccionarEstado);
          }
        }, 100);
      });
  

      return {
      //mapa
        svgMapa,
        estadoSeleccionado,
        infoEstados,
        resetSeleccion,
    //Tablas
    //  chartData: {
    //     labels: ['30 a 40', '40 a 50', '50 a 60', '60 a 70', '70 a 80', 'Mayor a 80'],
    //     datasets: [
    //       {
    //         label: 'Número de personas',
    //         backgroundColor: ['#4b0082', '#800080', '#e75480', '#ff69b4', '#ffb6c1'],
    //         data: [5, 10, 15, 30, 20, 22]  
    //       }
    //     ]
    //   },
    //   chartOptions: {
    //     indexAxis: 'y',  // barras  horizontales
    //     responsive: true,
    //     plugins: {
    //       legend: {
    //         display: false  
    //       }
    //     },
    //     scales: {
    //       x: {
    //         beginAtZero: true
    //       }
    //     }
    //   }
      };
    }
  };
  </script>
  
  <style scoped>
  .mapa-container {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }
  .mapa-svg {
    width: 70%;
  }
  .mapa-svg :deep(svg) {
    width: 100%;
    height: auto;
  }
  .mapa-svg :deep(path) {
    cursor: pointer;
    transition: fill 0.3s;
  }
  .mapa-svg :deep(path:hover) {
    fill: #0066cc;
  }
  .info-estado {
    width: 25%;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  </style>