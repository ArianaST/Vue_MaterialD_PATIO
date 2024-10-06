<script setup>
// example components
import TransparentBlogCard from "../../../../examples/cards/blogCards/TransparentBlogCard.vue";
import BackgroundBlogCard from "../../../../examples/cards/blogCards/BackgroundBlogCard.vue";

//Vue Material Kit 2 components
import post1 from "@/assets/img/examples/testimonial-6-2.jpg";
import post2 from "@/assets/img/examples/testimonial-6-3.jpg";
import post3 from "@/assets/img/examples/blog-9-4.jpg";
import post4 from "@/assets/img/examples/blog2.jpg";
</script>
<template>
  <section class="py-4">
    <div class="container">
      <div class="row ">
        <div class="d-flex flex-column text-center p-3 mb-3">
          <div class="d-flex mx-auto text-center">
          <h2 class="mb-2">Cono</h2>
          <h2 class="text-gradient text-primary mb-0">cenos</h2>
        </div>
          <p clas="mb-0" >Somos un equipo de investigadores, organizaciones y desarrolladores......</p>
        </div>
      </div>
      <div class="row flex-wrap justify-content-between">
        <div class="col-lg-3 col-sm-6">
          <TransparentBlogCard
            :image="post1"
            title="Investigadores"
            description="Finding temporary housing for your dog should be as easy as renting an Airbnb. That’s the idea behind Rover ..."
          />
        </div>
        <div class="col-lg-3 col-sm-6">
          <TransparentBlogCard
            :image="post2"
            title="Organizaciones"
            description="If you’ve ever wanted to train a machine learning model and integrate it with IFTTT, you now can with ..."
          />
        </div>
        <div class="col-lg-3 col-sm-6">
          <TransparentBlogCard
            :image="post3"
            title="Pacientes"
            description="If you’ve ever wanted to train a machine learning model and integrate it with IFTTT, you now can with ..."
          />
        </div>
        
      </div>
    </div>
  </section>
</template>
