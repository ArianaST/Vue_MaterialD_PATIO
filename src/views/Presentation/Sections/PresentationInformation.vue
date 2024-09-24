<script setup>
import RotatingCard from "../../../examples/cards/rotatingCards/RotatingCard.vue";
import RotatingCardFront from "../../../examples/cards/rotatingCards/RotatingCardFront.vue";
import RotatingCardBack from "../../../examples/cards/rotatingCards/RotatingCardBack.vue";

</script>
<template>
  <section class=" py-5">
    <div class="container">
      <div class="row d-flex flex-wrap justify-content-between ">
        <h2 class="mb-5 text-center">Nuestros blogs </h2>
        <div class="col-lg-4 col-md-6 mb-4">
          <RotatingCard >
            <RotatingCardFront
              image="https://blog.laboratorioslegrand.com/hs-fs/hubfs/Imagenes%20Blog/enfermedad%20de%20Parkinson.jpeg?width=1060&height=504&name=enfermedad%20de%20Parkinson.jpeg"
              icon="touch_app"
              title="¿Qué es <br/> la Enfermedad de Parkinson?"
      
            />
            <RotatingCardBack
              image="https://blog.laboratorioslegrand.com/hs-fs/hubfs/Imagenes%20Blog/enfermedad%20de%20Parkinson.jpeg?width=1060&height=504&name=enfermedad%20de%20Parkinson.jpeg"
              description="You will save a lot of time going from prototyping to full-functional code because all elements are implemented."
              :action="[
                {
                  color:'primary',
                  route: './/sections/page-sections/hero-sections.html',
                  label: 'Leer más',
                },
              ]"
            />
          </RotatingCard>
        </div>

          <div class="col-lg-4 col-md-6 mb-4">
          <RotatingCard>
            <RotatingCardFront
              image="https://prensa.css.gob.pa/wp-content/uploads/2021/04/PARKINSON.jpg"
              icon="touch_app"
              title="Daño a nivel <br/> cerebral a causa del Parkinson"
            
            />

            <RotatingCardBack
              image="https://prensa.css.gob.pa/wp-content/uploads/2021/04/PARKINSON.jpg"
              description="You will save a lot of time going from prototyping to full-functional
                code because all elements are implemented."
              :action="[
                {
                  color:'primary',
                  route: './/sections/page-sections/hero-sections.html',
                  label: 'Leer más',
                },
              ]"
            />
          </RotatingCard>
          </div>

          <div class="col-lg-4 col-md-6 mb-4">
     <RotatingCard>
            <RotatingCardFront
              image="https://www.scielo.org.mx/img/revistas/spm/v62n6//0036-3634-spm-62-06-873-gf1.png"
              icon="touch_app"
              title="Datos oficiales <br /> de la Enfermedad de Parkinson"

            />

            <RotatingCardBack
              image="https://www.scielo.org.mx/img/revistas/spm/v62n6//0036-3634-spm-62-06-873-gf1.png"
              description="You will save a lot of time going from prototyping to full-functional
                code because all elements are implemented."
              :action="[
                {
                  color:'primary',
                  route: './/sections/page-sections/hero-sections.html',
                  label: 'Leer más',
                
                },
              ]"
            />
          </RotatingCard>
        </div>
        
        <div class="col-lg-4 col-md-6 mb-4">
     <RotatingCard>
            <RotatingCardFront
              image="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRBoIKLyKKRnh7fTzTm6lI9-YdGNsVMsBYGiQ&s"
              icon="touch_app"
              title="Estudios recientes  de la Enfermedad de Parkinson"

            />

            <RotatingCardBack
              image="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRBoIKLyKKRnh7fTzTm6lI9-YdGNsVMsBYGiQ&s"
              description="You will save a lot of time going from prototyping to full-functional
                code because all elements are implemented."
              :action="[
                {
                  color:'primary',
                  route: './/sections/page-sections/hero-sections.html',
                  label: 'Leer más',
                
                },
              ]"
            />
          </RotatingCard>
        </div>

        <div class="col-lg-4 col-md-6 mb-4">
     <RotatingCard>
            <RotatingCardFront
              image="https://www.parkinson.org/sites/default/files/styles/no_sizing/public/images/environmentalfactors.jpg?itok=pZYM0ncD"
              icon="touch_app"
              title="Factores de riesgo de la Enfermedad de Parkinson"

            />

            <RotatingCardBack
              image="https://www.parkinson.org/sites/default/files/styles/no_sizing/public/images/environmentalfactors.jpg?itok=pZYM0ncDg"
              description="You will save a lot of time going from prototyping to full-functional
                code because all elements are implemented."
              :action="[
                {
                  color:'primary',
                  route: './/sections/page-sections/hero-sections.html',
                  label: 'Leer más',
                
                },
              ]"
            />
          </RotatingCard>
        </div>

        <div class="col-lg-4 col-md-6 mb-4">
     <RotatingCard>
            <RotatingCardFront
              image="https://quantifyresearch.com/wp-content/uploads/2021/04/shutterstock_1937510500-2.jpg"
              icon="touch_app"
              title="Día mundial de la Enfermedad de Parkinson"

            />

            <RotatingCardBack
              image="https://quantifyresearch.com/wp-content/uploads/2021/04/shutterstock_1937510500-2.jpg"
              description="You will save a lot of time going from prototyping to full-functional
                code because all elements are implemented."
              :action="[
                {
                  color:'primary',
                  route: './/sections/page-sections/hero-sections.html',
                  label: 'Leer más',
                
                },
              ]"
            />
          </RotatingCard>
        </div>

      </div>
    </div>
  </section>
</template>
