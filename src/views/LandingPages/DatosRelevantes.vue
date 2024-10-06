<template>
  <section class="data-display">
    <p class="mb-0"> ¡Conoce cuantas personas han participado! </p>
    <div class="logo-container">
      <img src="@/assets/img/PATITO.png" alt="PaTO Logo" class="logo" />
      <h2 class="mb-0">PATITO</h2>
    </div>
    <div class="info-cards">
      <div class="card total-records">
        <h3>Registros totales</h3>
        <p>{{ totalRecords }}</p>
      </div>
      <div class="card most-records">
        <h3>Estado con más registros</h3>
        <p>{{ stateWithMostRecords }}</p>
      </div>
      <div class="card least-records">
        <h3>Estado con menos registros</h3>
        <p>{{ stateWithLeastRecords }}</p>
      </div>
    </div>
    <p class="call-to-action">
      Aún necesitamos muchos registros. ¡No dejes de participar!
    </p>
    <p class="subtext">
      Con tú participación ayudamos al desarrollo de la Enfermedad de Parkinson
      en México.
    </p>
  </section>
</template>

 <script>

export default {
  data() {
    return {
      totalRecords: 0,
      stateWithMostRecords: '',
      stateWithLeastRecords: ''
    };
  },
  methods: {
    fetchData() {
      //  obtener datos de la base de datos
      this.totalRecords = 'Provisional';
      this.stateWithMostRecords = 'Provisional';
      this.stateWithLeastRecords = 'Provisional';
    }
  },
  mounted() {
    this.fetchData();
  },
}
</script>

<style scoped>
/* Ajuste general de la sección */
.data-display {
  text-align: center;
  padding: 20px;
}

.logo-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.logo {
  width: 180px;
  margin-bottom: 10px;
}

.info-cards {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-bottom: 20px;
  flex-wrap: wrap; 
}

.card {
  background-color: #f5f5f5;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  flex: 1;
  max-width: 400px;
  min-width: 280px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.total-records {
  background-color: #8b0000;
  color: white;
}

.most-records {
  background-color: #ffcccb;
}

.least-records {
  background-color: #ffe4e1;
}

h3 {
  font-size: 1.2em;
  margin-bottom: 10px;
}

p {
  font-size: 2em;
  font-weight: bold;
}

.card:hover,
.card:active {
  transform: translateY(-10px); /* Levanta la tarjeta */
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2); /* Aumenta la sombra */
}

@media (max-width: 768px) {
  .info-cards {
    flex-direction: column; /* Las tarjetas se apilan verticalmente */
  }

  .card {
    margin-bottom: 20px; 
  }
}

.call-to-action {
  margin-top: 20px;
  font-size: 1.1em;
  font-weight: bold;
}

.subtext {
  margin-top: 10px;
  font-size: 0.9em;
  color: #555;
}

</style>
