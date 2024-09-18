<template>
    <div class="section-benefits">
      <h2>¿Quiénes se benefician en estos datos?</h2>
      <p class="sub-text">Regular Text - Lorem ipsum dolor sit amet, consectetur</p>
      <div class="benefit-steps">
        <div class="step" v-for="(step, index) in steps" :key="index">
          <div class="icon-circle">
            <img :src="step.icon" alt="icon" />
          </div>
          <h3>{{ step.title }}</h3>
          <p>{{ step.text }}</p>
        </div>
      </div>
    </div>
  </template>

<script>
export default {
  data() {
    return {
      steps: [
        {
          icon: "",
          title: "Submit your entry",
          text: "Regular Text - Lorem ipsum dolor sit amet, consectetur"
        },
        {
          icon: "",
          title: "Vote for other entries",
          text: "Regular Text - Lorem ipsum dolor sit amet, consectetur"
        },
        {
          icon: "",
          title: "Like our fanpage",
          text: "Regular Text - Lorem ipsum dolor sit amet, consectetur"
        },
        {
          icon: "",
          title: "Share it with friends",
          text: "Regular Text - Lorem ipsum dolor sit amet, consectetur"
        }
      ]
    };
  }
};
</script>

<style scoped>
.section-benefits {
  text-align: center;
  padding: 2rem;
}

.sub-text {
  font-size: 1.2rem;
  color: #7d8da1;
  margin-bottom: 2rem;
}

.benefit-steps {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-top: 2rem;
}

.step {
  max-width: 200px;
}

.icon-circle {
  background-color: #f0f4f8;
  border-radius: 50%;
  width: 80px;
  height: 80px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto 1rem;
}

.icon-circle img {
  width: 40px;
  height: 40px;
}

h3 {
  font-size: 1rem;
  font-weight: 600;
  color: #333;
  margin: 0.5rem 0;
}

p {
  font-size: 0.9rem;
  color: #7d8da1;
}
</style>
