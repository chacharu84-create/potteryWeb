<script setup>
import { ref, computed, watch, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import ArticleCard from '../components/ArticleCard.vue'

const route = useRoute()
const allArticles = ref([])
const categories = ref([])

const PAGE_SIZE = 5
const currentPage = ref(1)

const categoryId = computed(() => route.params.categoryId)

const currentCategory = computed(() =>
  categories.value.find((c) => c.id === categoryId.value)
)

const filteredArticles = computed(() =>
  allArticles.value
    .filter((a) => a.categoryId === categoryId.value)
    .sort((a, b) => new Date(b.date) - new Date(a.date))
)

const totalPages = computed(() =>
  Math.ceil(filteredArticles.value.length / PAGE_SIZE)
)

const pagedArticles = computed(() => {
  const start = (currentPage.value - 1) * PAGE_SIZE
  return filteredArticles.value.slice(start, start + PAGE_SIZE)
})

watch(categoryId, () => {
  currentPage.value = 1
})

onMounted(async () => {
  try {
    const [artRes, catRes] = await Promise.all([
      fetch(import.meta.env.BASE_URL + 'articleList.json'),
      fetch(import.meta.env.BASE_URL + 'category.json'),
    ])
    allArticles.value = await artRes.json()
    categories.value = await catRes.json()
  } catch (e) {
    console.error('無法載入資料', e)
  }
})
</script>

<template>
  <div class="list-page">
    <div class="container">
      <!-- 分類標題 -->
      <div class="category-header">
        <h1 class="category-title">
          {{ currentCategory ? currentCategory.name : '文章清單' }}
        </h1>
        <p v-if="currentCategory" class="category-desc">
          {{ currentCategory.description }}
        </p>
      </div>

      <!-- 文章清單 -->
      <div v-if="pagedArticles.length" class="article-list">
        <ArticleCard
          v-for="article in pagedArticles"
          :key="article.id"
          :article="article"
        />
      </div>
      <div v-else class="no-articles">
        <p>此分類尚無文章</p>
      </div>

      <!-- 分頁 -->
      <div v-if="totalPages > 1" class="pagination">
        <button
          class="page-btn"
          :disabled="currentPage === 1"
          @click="currentPage--"
        >
          ‹
        </button>
        <button
          v-for="p in totalPages"
          :key="p"
          class="page-btn"
          :class="{ active: p === currentPage }"
          @click="currentPage = p"
        >
          {{ p }}
        </button>
        <button
          class="page-btn"
          :disabled="currentPage === totalPages"
          @click="currentPage++"
        >
          ›
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.list-page {
  min-height: 80vh;
  padding: 3rem 0 5rem;
}

.container {
  max-width: 860px;
  margin: 0 auto;
  padding: 0 2rem;
}

.category-header {
  margin-bottom: 2.5rem;
}

.category-title {
  font-size: 2rem;
  font-weight: 800;
  color: #222;
  margin-bottom: 0.5rem;
}

.category-desc {
  font-size: 0.9rem;
  color: #888;
}

.article-list {
  /* cards separated by border-bottom inside ArticleCard */
}

.no-articles {
  padding: 4rem 0;
  text-align: center;
  color: #aaa;
  font-size: 0.95rem;
}

/* ── Pagination ── */
.pagination {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  margin-top: 3rem;
}

.page-btn {
  min-width: 36px;
  height: 36px;
  padding: 0 10px;
  border: 1px solid #ddd;
  background: #fff;
  border-radius: 4px;
  cursor: pointer;
  font-family: 'Microsoft JhengHei', '微軟正黑體', sans-serif;
  font-size: 0.9rem;
  color: #555;
  transition: all 0.15s;
}
.page-btn:hover:not(:disabled) {
  border-color: #C8342A;
  color: #C8342A;
}
.page-btn.active {
  background: #C8342A;
  border-color: #C8342A;
  color: #fff;
}
.page-btn:disabled {
  opacity: 0.35;
  cursor: not-allowed;
}
</style>
