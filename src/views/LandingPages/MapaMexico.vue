<template>
  <div class="ContainerTabs">
      <div class="mapa-container">
      <div class="mapa-svg" v-html="svgMapa" @click="resetSeleccion"></div>
      <div v-if="estadoSeleccionado" class="info-estado">
        <h2>{{ infoEstados[estadoSeleccionado]?.nombre }}</h2>
        <p>Capital: {{ infoEstados[estadoSeleccionado]?.capital }}</p>
        <p>Total de registros: {{ infoEstados[estadoSeleccionado]?.registros }}</p>
      </div>
    </div>

  </div>
  </template>
  
  <script>
  import { registerRuntimeCompiler } from 'vue';
import { ref, onMounted } from 'vue';
import Registro from './Registro.vue';
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
        MXSON: { nombre: "Sonora", capital: "Hermosillo", registros: "2" },
        MXBCN: { nombre: "Baja California", capital: "Mexicali", registros: "redacted" },
        MXCHH: { nombre: "Chihuahua", capital: "Chihuahua", registros: "redacted" },
        MXCOA: { nombre: "Coahuila", capital: "Saltillo", registros: "redacted" },
        MXTAM: { nombre: "Tamaulipas", capital: "Ciudad Victoria", registros: "redacted" },
        MXNLE: { nombre: "Nuevo León", capital: "Monterrey", registros: "redacted" },
        MXROO: { nombre: "Quintana Roo", capital: "Chetumal", registros: "redacted" },
        MXCAM: { nombre: "Campeche", capital: "Campeche", registros: "redacted" },
        MXTAB: { nombre: "Tabasco", capital: "Villahermos", registros: "redacted" },
        MXCHP: { nombre: "Chiapas", capital: "Tuxtla Gutiérrez", registros: "redacted" },
        MXCOL: { nombre: "Colima", capital: "Colima", registros: "redacted" },
        MXNAY: { nombre: "Nayarit", capital: "Tepic", registros: "redacted" },
        MXBCS: { nombre: "Baja California Sur", capital: "La Paz", registros: "redacted" },
        MXSIN: { nombre: "Sinaloa", capital: "Culiacán Rosales", registros: "redacted" },
        MXYUC: { nombre: "Yucatán", capital: "Mérida", registros: "redacted" },
        MXVER: { nombre: "Veracruz", capital: "Xalapa", registros: "redacted" },
        MXJAL: { nombre: "Jalisco", capital: "Guadalajara", registros: "redacted" },
        MXMIC: { nombre: "Michoacán", capital: "Morelia", registros: "redacted" },
        MXGRO: { nombre: "Guerrero", capital: "Chilpancingo", registros: "redacted" },
        MXOAX: { nombre: "Oaxaca", capital: "Oaxaca de Juárez", registros: "redacted" },
        MXMEX: { nombre: "México", capital: "México", registros: "redacted" },
        MXPUE: { nombre: "Puebla", capital: "Puebla de Zaragoza", registros: "redacted" },
        MXMOR: { nombre: "Morelos", capital: "Cuernavaca", registros: "redacted" },
        MXQUE: { nombre: "Querétaro", capital: "Santiago de Querétaro", registros: "redacted" },
        MXHID: { nombre: "Hidalgo", capital: "Pachuca", registros: "redacted" },
        MXGUA: { nombre: "Guanajuato", capital: "Guanajuato", registros: "redacted" },
        MXSLP: { nombre: "San Luis Potosí", capital: "San Luis Potosí", registros: "redacted" },
        MXZAC: { nombre: "Zacatecas", capital: "Zacatecas", registros: "redacted" },
        MXAGU: { nombre: "Aguascalientes", capital: "Aguascalientes", registros: "redacted" },
        MXDUR: { nombre: "Durango", capital: "Durango", registros: "redacted" },
        MXTLA: { nombre: "Tlaxcala", capital: "Tlaxcala", registros: "redacted" },
        MXCMX: { nombre: "Ciudad de México", capital: "Ciudad de México", registros: "redacted" },
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
    border: 2px solid #ccc;
    border-radius: 5px;
  }
  </style>