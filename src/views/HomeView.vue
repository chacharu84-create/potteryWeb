<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import CategoryCard from '../components/CategoryCard.vue'

const router = useRouter()
const categories = ref([])
const baseUrl = import.meta.env.BASE_URL

onMounted(async () => {
  try {
    const res = await fetch(import.meta.env.BASE_URL + 'category.json')
    categories.value = await res.json()
  } catch (e) {
    console.error('無法載入分類', e)
  }
})

function goToCategory(id) {
  router.push(`/articles/${id}`)
}
</script>

<template>
  <!-- Hero 大圖區 -->
  <section class="hero">
    <img :src="baseUrl + 'images/hero.jpg'" alt="土手製陶 Hero" class="hero-img" />
  </section>

  <!-- 分類卡片區 -->
  <section class="categories-section">
    <div class="container">
      <div class="categories-grid">
        <div
          v-for="cat in categories"
          :key="cat.id"
          class="category-item"
          @click="goToCategory(cat.id)"
        >
          <CategoryCard :category="cat" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* ── Hero ── */
.hero {
  width: 100%;
  line-height: 0;
}

.hero-img {
  width: 100%;
  height: auto;
  display: block;
  max-height: 560px;
  object-fit: cover;
  object-position: center center;
}

/* ── Categories ── */
.categories-section {
  background: #F5F5F5;
  padding: 4rem 0;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 2rem;
}

.categories-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.category-item {
  cursor: pointer;
}

@media (max-width: 768px) {
  .hero-img {
    max-height: 280px;
    object-position: left center;
  }
  .categories-grid {
    grid-template-columns: 1fr;
  }
}
</style>
