<template>
    <div class="form-container">
      <h2>Por favor, lee con atención y completa los siguientes datos:</h2>
      
      <div class="tabs">
        <button 
          v-for="tab in tabs" 
          :key="tab.id" 
          @click="currentTab = tab.id"
          :class="{ active: currentTab === tab.id }"
        >
          {{ tab.name }}
        </button>
      </div>
  
      <div v-if="currentTab === '01'" class="tab-content">
        <h3>01. Datos demográficos</h3>
        <div class="form-group">
          <label for="nombre">Nombre(s):</label>
          <input type="text" id="nombre" v-model="formData.nombre">
        </div>
        <div class="form-group">
          <label for="apellidoPaterno">Apellido paterno:</label>
          <input type="text" id="apellidoPaterno" v-model="formData.apellidoPaterno">
        </div>
        <div class="form-group">
          <label for="apellidoMaterno">Apellido materno:</label>
          <input type="text" id="apellidoMaterno" v-model="formData.apellidoMaterno">
        </div>
        <div class="form-group">
          <label for="fechaNacimiento">Fecha de nacimiento:</label>
          <input type="date" id="fechaNacimiento" v-model="formData.fechaNacimiento">
        </div>
        <div class="form-group">
          <label for="edad">Edad:</label>
          <select id="edad" v-model="formData.edad">
            <option value="">Seleccione</option>
            <option v-for="edad in edades" :key="edad" :value="edad">{{ edad }}</option>
          </select>
        </div>
        <div class="form-group">
          <label for="ocupacion">Ocupación:</label>
          <input type="text" id="ocupacion" v-model="formData.ocupacion">
        </div>
        <div class="form-group">
          <label for="genero">Género:</label>
          <select id="genero" v-model="formData.genero">
            <option value="">Seleccione</option>
            <option v-for="gen in generos" :key="gen" :value="gen">{{ gen }}</option>
          </select>
        </div>
        <div class="form-group">
          <label for="estadoNacimiento">Estado de nacimiento:</label>
          <select id="estadoNacimiento" v-model="formData.estadoNacimiento">
            <option value="">Seleccione</option>
            <option v-for="estado in estadosNacimiento" :key="estado" :value="estado">{{ estado }}</option>
          </select>
        </div>
      </div>
  
      <div v-if="currentTab === '02'" class="tab-content">
        <h3>02. Historia médica</h3>
        <div class="form-group">
          <label>¿Actualmente se encuentra registrado en algun centro clinico neurólogo?:</label>
          <div>
            <input type="radio" id="tratamientoSi" value="si" v-model="formData.bajoTratamiento">
            <label for="tratamientoSi">Sí</label>
          </div>
          <div>
            <input type="radio" id="tratamientoNo" value="no" v-model="formData.bajoTratamiento">
            <label for="tratamientoNo">No</label>
          </div>
        </div>
        <div class="form-group" v-if="formData.bajoTratamiento === 'si'">
          <label for="medicacion">¿Cuál es su medicación?</label>
          <input type="text" id="medicacion" v-model="formData.medicacion">
        </div>
        <div class="form-group">
          <label>Sabe cual es su escala especifica en la Escala Unificada de Calificación de la Enfermedad de Parkinson (MDS-UPDRS)?</label>
          <div>
            <input type="radio" id="escalasSi" value="si" v-model="formData.EscalaMedicion">
            <label for="escalaSi">Sí</label>
          </div>
          <div>
            <input type="radio" id="escalaNo" value="no" v-model="formData.EscalaMedicion">
            <label for="escalaNo">No</label>
          </div>
        </div>
        <div class="form-group" v-if="formData.EscalaMedicion === 'si'">
          <label for="MDS_UPDRS">¿Cuál es su MDS-UPDRS Total?</label>
          <input type="text" id="MDS_UPDRS" v-model="formData.MDS_UPDRS">
        </div>
      </div>
      <div v-if="currentTab === '03'" class="tab-content">
      <h3>03. Función cognitiva</h3>
      <div class="form-group">
        <label for="imagen1">Imagen 1:</label>
        <input type="file" id="imagen1" @change="onFileSelected($event, 'imagen1')" accept="image/*">
        <img v-if="formData.imagen1" :src="formData.imagen1" alt="Vista previa imagen 1" class="preview-image">
      </div>

      <div class="form-group">
        <label for="imagen2">Imagen 2:</label>
        <input type="file" id="imagen2" @change="onFileSelected($event, 'imagen2')" accept="image/*">
        <img v-if="formData.imagen2" :src="formData.imagen2" alt="Vista previa imagen 2" class="preview-image">
      </div>

      <div class="form-group">
        <label for="video">Video (Webcam):</label>
        <button @click="startWebcam" v-if="!isRecording">Iniciar Webcam</button>
        <button @click="stopWebcam" v-if="isRecording">Detener y Guardar</button>
        <video ref="webcam" v-show="isRecording" autoplay></video>
        <img v-if="formData.video" :src="formData.video" alt="GIF capturado" class="preview-video">
      </div>
    </div>
      <button @click="guardarDatos" class="btn-guardar">Guardar Datos</button>
    </div>
  </template>
  
  <script>
  import GIF from 'gif.js';
  export default {
    data() {
      return {
        currentTab: '01',
        tabs: [
          { id: '01', name: '01. Datos demográficos' },
          { id: '02', name: '02. Historia médica' },
          { id: '03', name: '03. Función cognitiva' },
          { id: '04', name: '04. Factores ambientales' },
          { id: '05', name: '05. Uso y abuso de sustancias' },
        ],
        formData: {
          nombre: '',
          apellidoPaterno: '',
          apellidoMaterno: '',
          fechaNacimiento: '',
          edad: '',
          ocupacion: '',
          genero: '',
          estadoNacimiento: '',
          bajoTratamiento: '',
          medicacion: '',
          EscalaMedicion:'',
          MDS_UPDRS: '',
          video: null,
        },
        isRecording: false,
        mediaStream: null,
        gifRecorder: null,
        edades: Array.from({length: 120}, (_, i) => i + 1),
        generos: ['Masculino', 'Femenino', 'Otro'],
        estadosNacimiento: [
          'Aguascalientes', 'Baja California', 'Baja California Sur', 'Campeche',
          'Chiapas', 'Chihuahua', 'Coahuila', 'Colima', 'Durango', 'Guanajuato',
          'Guerrero', 'Hidalgo', 'Jalisco', 'México', 'Michoacán', 'Morelos',
          'Nayarit', 'Nuevo León', 'Oaxaca', 'Puebla', 'Querétaro', 'Quintana Roo',
          'San Luis Potosí', 'Sinaloa', 'Sonora', 'Tabasco', 'Tamaulipas', 'Tlaxcala',
          'Veracruz', 'Yucatán', 'Zacatecas', 'Ciudad de México'
        ]
      }
    },
    methods: {
      onFileSelected(event, field) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.formData[field] = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    },
    async startWebcam() {
      try {
        this.mediaStream = await navigator.mediaDevices.getUserMedia({ video: true });
        this.$refs.webcam.srcObject = this.mediaStream;
        this.isRecording = true;
        this.startRecording();
      } catch (error) {
        console.error('Error accessing webcam:', error);
      }
    },
    startRecording() {
      this.gifRecorder = new GIF({
        workers: 2,
        quality: 10,
        width: 320,
        height: 240
      });

      const captureFrame = () => {
        if (this.isRecording) {
          this.gifRecorder.addFrame(this.$refs.webcam, {copy: true, delay: 100});
          setTimeout(captureFrame, 100);
        }
      };

      captureFrame();
    },
    stopWebcam() {
      this.isRecording = false;
      if (this.mediaStream) {
        this.mediaStream.getTracks().forEach(track => track.stop());
      }
      this.gifRecorder.on('finished', (blob) => {
        this.formData.video = URL.createObjectURL(blob);
      });
      this.gifRecorder.render();
    },
    guardarDatos() {
      const datosParaGuardar = { ...this.formData };
      ['imagen1', 'imagen2', 'video'].forEach(field => {
        if (datosParaGuardar[field]) {
          datosParaGuardar[field] = `[${field} cargado]`;
        }
      });
      
      console.log('Datos del formulario:', JSON.stringify(datosParaGuardar, null, 2));
      }
    }
  }
  </script>
  
<style scoped>
.form-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.tabs {
  display: flex;
  margin-bottom: 20px;
}

.tabs button {
  padding: 10px 15px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
}

.tabs button.active {
  background-color: #4b5764;
  color: white;
}

.tab-content {
  border: 1px solid #ddd;
  padding: 20px;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="text"],
input[type="date"],
select {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
.btn-guardar {
    background-color: #28a745;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    margin-top: 20px;
  }
  
  .btn-guardar:hover {
    background-color: #218838;
  }
  .preview-image, .preview-video {
  max-width: 200px;
  max-height: 200px;
  margin-top: 10px;
}
preview-video {
  max-width: 320px;
  max-height: 240px;
  margin-top: 10px;
}
</style>



