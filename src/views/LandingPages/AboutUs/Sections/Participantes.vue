<template>
    <div class="participants-section">
      <h2>PARTICIPANTES E INVESTIGADORES</h2>
      <div class="card-grid">
        <div class="card" v-for="(article, index) in articles" :key="index">
          <div class="image-placeholder">
            <img :src="article.image" alt="Article Image" />
          </div>
          <h3>{{ article.title }}</h3>
          <p class="author">{{ article.author }} &middot; {{ article.date }} &middot; {{ article.readTime }}</p>
          <p class="description">{{ article.description }}</p>
        </div>
      </div>
    </div>
  </template>

<style scoped>
.participants-section {
  text-align: center;
  padding: 2rem;
}

h2 {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 2rem;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.card {
  background-color: #f8f9fa;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  text-align: left;
}

.image-placeholder {
  background-color: #e9ecef;
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  margin-bottom: 1rem;
}

.image-placeholder img {
  max-width: 100%;
  max-height: 100%;
}

h3 {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.author {
  font-size: 0.9rem;
  color: #6c757d;
  margin-bottom: 1rem;
}

.description {
  font-size: 0.9rem;
  color: #6c757d;
}
</style>


<script>
export default {
  data() {
    return {
      articles: [
        {
          image: "path_to_image_1",
          title: "How to Overcome Creative Blocks & Find Inspiration",
          author: "Ana Maria Lopez",
          date: "Mar 15, 2022",
          readTime: "10 min read",
          description: "Suspendisse potenti. Sed neque augue, mattis in posuere quis, sagittis..."
        },
        {
          image: "path_to_image_2",
          title: "Unusual Uses for Everyday Household Items",
          author: "Bob Jones",
          date: "Feb 18, 2022",
          readTime: "9 min read",
          description: "Nunc mi tortor, venenatis fermentum ipsum id, gravida lacinia carta..."
        },
        {
          image: "path_to_image_3",
          title: "Spectacular Natural Wonders Everyone Should See",
          author: "John Alvarez",
          date: "Mar 18, 2022",
          readTime: "16 min read",
          description: "Praesent lobortis, lorem id elementum vehicula, sapien ipsum tincidunt..."
        },
        {
          image: "path_to_image_4",
          title: "How to Overcome Creative Blocks & Find Inspiration",
          author: "Ana Maria Lopez",
          date: "Mar 15, 2022",
          readTime: "10 min read",
          description: "Suspendisse potenti. Sed neque augue, mattis in posuere quis, sagittis..."
        },
        {
          image: "path_to_image_5",
          title: "How to Overcome Creative Blocks & Find Inspiration",
          author: "Ana Maria Lopez",
          date: "Mar 15, 2022",
          readTime: "10 min read",
          description: "Suspendisse potenti. Sed neque augue, mattis in posuere quis, sagittis..."
        }
      ]
    };
  }
};
</script>
