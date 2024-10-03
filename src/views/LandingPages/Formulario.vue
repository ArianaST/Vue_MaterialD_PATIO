<template>
  <div class="form-container">
    <h2>Por favor, lee con atención y completa los siguientes datos:</h2>
    
    <div class="tabs mt-2">
      <button 
        v-for="tab in tabs" 
        :key="tab.id" 
        @click="currentTab = tab.id"
        :class="{ active: currentTab === tab.id }"
      >
        {{ tab.name }}
      </button>
    </div>

    <div v-if="currentTab === '01'" class="tab-content mt-2">
      <h3>01. Datos demográficos</h3>
      <div class="form-group">

        <div class="row justify-space-between py-2">
        <div class="col-lg-4 mx-auto">
          <MaterialInput
            class="input-group-static mb-4"
            label="First Name"
            type="text"
            placeholder="eg. Thomas Shelby"
            v-model="formData.nombre"
          />
        </div>
      </div>

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
      <div class="form-group">
        <label for="estadoRecidencia">Estado de residencia:</label>
        <select id="estadoRecidencia" v-model="formData.estadoRecidencia">
          <option value="">Seleccione</option>
          <option v-for="estado in estadosRecidencia" :key="estado" :value="estado">{{ estado }}</option>
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
    <div class="form-group py-3 ">
      <h6> Si ya cuentas con imagenes de espirales y ondas subirlas en los apartados de a continuación: </h6>
      <label  class="text-center py-3" for="imagen1"> SUBIR IMAGEN DE ESPIRAL:</label>
      <input type="file" id="imagen1" @change="onFileSelected($event, 'imagen1')" accept="image/*">
      <img v-if="formData.imagen1" :src="formData.imagen1" alt="Vista previa imagen 1" class="preview-image">
    </div>

    <div class="form-group py-4">
      <label class="text-center py-3" for="imagen2">SUBIR IMAGEN DE ONDA:</label>
      <input type="file" id="imagen2" @change="onFileSelected($event, 'imagen2')" accept="image/*">
      <img v-if="formData.imagen2" :src="formData.imagen2" alt="Vista previa imagen 2" class="preview-image">
    </div>

    <h6 clas="py-5"> EN CASO DE NO CONTAR CON IMAGENES, A CONTINUACIÓN SE PEDIRA QUE DIBUJE UNA ONDA Y UNA ESPIRAL EN  LOS SIGUIENTES ESPACIOS SIN SALIRSE DEL RECUADRO, AL TERMINAR	PRESIONAR EN GUARDAR EN CADA CASO:</h6>
    <div class="canvas-container">
        <div class="canvas-item">
          <h4 class="text-center">Dibujar Espiral</h4>
          <canvas ref="canvasOnda" width="330" height="300" class="canvas" @mousemove="checkInitCanvas('onda')"></canvas>
          <div class="button-group">
            <button @click="clearCanvas('onda')">Borrar Espiral</button>
            <button @click="saveCanvas('onda')">Mandar Espiral</button>
          </div>
          <img v-if="formData.onda" :src="formData.onda" alt="Vista previa de Onda" class="preview-image">
        </div>

        <div class="canvas-item">
          <h4 class="text-center">Dibujar Onda</h4>
          <canvas ref="canvasEspiral" width="330" height="300" class="canvas" @mousemove="checkInitCanvas('espiral')"></canvas>
          <div class="button-group">
            <button @click="clearCanvas('espiral')">Borrar Onda</button>
            <button @click="saveCanvas('espiral')">Mandar Onda</button>
          </div>
          <img v-if="formData.espiral" :src="formData.espiral" alt="Vista previa de Espiral" class="preview-image">
        </div>
      </div>

      <h6 class="mt-5">SE PEDIRA PERMISOS PARA TENER ACCESO A LA CÁMARA DEL DISPOSITIVO EN USO PARA GRABAR SOLO 95 SEGUNDOS DE LA MANO DEL PACIENTE, CUANDO EL MISMO TERMINE SE DARA EN GUARDAR.</h6>
      <div class="form-group py-3">
      <label for="video">Video (Webcam):</label>
      <button @click="startWebcam" v-if="!isRecording">Iniciar Webcam</button>
      <button @click="stopWebcam" v-if="isRecording">Detener y Guardar</button>
      <video ref="webcam" v-show="isRecording" autoplay></video>
      <img v-if="formData.video" :src="formData.video" alt="GIF capturado" class="preview-video">
    </div>


  </div>

  <div class="form-check form-switch py-4">
    <input
      :id="id"
      class="form-check-input"
      type="checkbox"
      :name="id"
      :checked="checked"
    />
    <label> He leído el AVISO DE PRIVACIDAD y estoy de acuerdo con el mismo para iniciar el regristro, asimismo este se encuentra completo para descargar en: link</label>
  </div>

  <div class="form-check form-switch mt-2">
    <input
      :id="id"
      class="form-check-input"
      type="checkbox"
      :name="id"
      :checked="checked"
    />
    <label> He firmado y acepto la carta de CONSENTIMIENTO informada, asimismo se encuentra completa para descargar en: link</label>
  </div>
  </div>
  <button @click="guardarDatos" class="btn-guardar mt-4">Guardar Datos</button>
</template>

<script>
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
        estadoRecidencia: '',
        bajoTratamiento: '',
        medicacion: '',
        EscalaMedicion:'',
        MDS_UPDRS: '',
        video: null,
        onda: null,
        espiral: null
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
      ],
      estadosRecidencia: [
        'Aguascalientes', 'Baja California', 'Baja California Sur', 'Campeche',
        'Chiapas', 'Chihuahua', 'Coahuila', 'Colima', 'Durango', 'Guanajuato',
        'Guerrero', 'Hidalgo', 'Jalisco', 'México', 'Michoacán', 'Morelos',
        'Nayarit', 'Nuevo León', 'Oaxaca', 'Puebla', 'Querétaro', 'Quintana Roo',
        'San Luis Potosí', 'Sinaloa', 'Sonora', 'Tabasco', 'Tamaulipas', 'Tlaxcala',
        'Veracruz', 'Yucatán', 'Zacatecas', 'Ciudad de México'
      ],
      isDrawing: false,
      contextOnda: null,
      contextEspiral: null,
      initializedCanvasOnda: false,
      initializedCanvasEspiral: false,
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
    ['imagen1', 'imagen2', 'video', 'onda', 'espiral', 'contextOnda', 'contextEspiral'].forEach(field => {
      if (datosParaGuardar[field]) {
        datosParaGuardar[field] = `[${field} cargado...]`;
      }
    });
    
    console.log('Datos del formulario:', JSON.stringify(datosParaGuardar, null, 2));
    },
    
    checkInitCanvas(type) {
      if (type === 'onda' && !this.initializedCanvasOnda) {
        this.initCanvasOnda();
        this.initializedCanvasOnda = true;
      } else if (type === 'espiral' && !this.initializedCanvasEspiral) {
        this.initCanvasEspiral();
        this.initializedCanvasEspiral = true;
      }
    },

    initCanvasOnda() {
      const canvasOnda = this.$refs.canvasOnda;
      this.contextOnda = canvasOnda.getContext('2d');
      canvasOnda.addEventListener('mousedown', this.startDrawingOnda);
      canvasOnda.addEventListener('mousemove', this.drawOnda);
      canvasOnda.addEventListener('mouseup', this.stopDrawingOnda);
    },

    initCanvasEspiral() {
      const canvasEspiral = this.$refs.canvasEspiral;
      this.contextEspiral = canvasEspiral.getContext('2d');
      canvasEspiral.addEventListener('mousedown', this.startDrawingEspiral);
      canvasEspiral.addEventListener('mousemove', this.drawEspiral);
      canvasEspiral.addEventListener('mouseup', this.stopDrawingEspiral);
    },
    startDrawingOnda(event) {
      this.isDrawing = true;
      this.contextOnda.beginPath();
      this.contextOnda.moveTo(event.offsetX, event.offsetY);
    },
    drawOnda(event) {
      if (!this.isDrawing) return;
      this.contextOnda.lineTo(event.offsetX, event.offsetY);
      this.contextOnda.stroke();
    },
    stopDrawingOnda() {
      this.isDrawing = false;
    },

    startDrawingEspiral(event) {
      this.isDrawing = true;
      this.contextEspiral.beginPath();
      this.contextEspiral.moveTo(event.offsetX, event.offsetY);
    },
    drawEspiral(event) {
      if (!this.isDrawing) return;
      this.contextEspiral.lineTo(event.offsetX, event.offsetY);
      this.contextEspiral.stroke();
    },
    stopDrawingEspiral() {
      this.isDrawing = false;
    },

    // Limpiar canvas
    clearCanvas(type) {
      if (type === 'onda') {
        this.contextOnda.clearRect(0, 0, 300, 300);
      } else if (type === 'espiral') {
        this.contextEspiral.clearRect(0, 0, 300, 300);
      }
    },

    // Guardar el dibujo del canvas
    saveCanvas(type) {
      if (type === 'onda') {
        this.formData.onda = this.$refs.canvasOnda.toDataURL('image/png');
      } else if (type === 'espiral') {
        this.formData.espiral = this.$refs.canvasEspiral.toDataURL('image/png');
      }
    },
  },
  
};
</script>

<style scoped>
.form-container {
  max-width: auto;
  padding: 20px;
  border: 2px solid #840705;
  border-radius: 10px;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
  color: dark;
}

/* Estilo de los tabs */
.tabs {
  position: center;
  margin-bottom: 30px;
}

.tabs button {
  padding: 10px 10px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
}

.tabs button.active {
  background-color: #840705;
  color: white;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

/* Estilo de los inputs */
input[type="text"],
input[type="date"],
select,
textarea {
  color: rgb(0, 0, 0);
  width: 100%;
  padding: 10px;
  border: 2px solid #a0a0a0; /* Cambia el color del borde de los inputs */
  border-radius: 5px;
  margin-bottom: 15px;
  font-size: 1rem;
}

textarea {
  resize: vertical;
}


button {
  color: rgb(0, 0, 0);
  background-color: #840705;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.carousel {
  border: 3px solid white;
  border-radius: 50%;
  box-shadow: 0 0 10px 2px rgba(255, 255, 255, 0.8);
}

.preview-image, .preview-video {
  max-width: 200px;
  max-height: 200px;
  margin-top: 10px;
  border: 1px solid #840705;
  border-radius: 10px;
}
.preview-video {
max-width: 320px;
max-height: 240px;
margin-top: 10px;
}

.canvas-container {
  display: flex;
  justify-content: center; /* Centrar los canvas en el eje horizontal */
  align-items: flex-start; /* Alinear los canvas en la parte superior */
  gap: 60px; /* Espacio entre los canvas */
  margin: 20px auto; /* Centrar el contenedor de los canvas */
  max-width: 800px; /* Limitar el ancho total para que no se peguen a los bordes */
}

.canvas-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.canvas {
  border: 1.5px solid #000;
  margin-bottom: 9px;
  width: 350px; /* Ajustar el tamaño del canvas si es necesario */
  height: 300px;
}

.button-group {
  display: flex;
  gap: 10px;
  justify-content: center; /* Alinear los botones al centro */
  margin-top: 10px;
}




</style>