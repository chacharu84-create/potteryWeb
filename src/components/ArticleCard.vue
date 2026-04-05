<script setup>
defineProps({
  article: {
    type: Object,
    required: true,
  },
})

const baseUrl = import.meta.env.BASE_URL

function formatDate(dateStr) {
  if (!dateStr) return ''
  const d = new Date(dateStr)
  const y = d.getFullYear()
  const m = String(d.getMonth() + 1).padStart(2, '0')
  const day = String(d.getDate()).padStart(2, '0')
  return `${y}.${m}.${day}`
}

function truncate(text, len = 100) {
  if (!text) return ''
  return text.length > len ? text.slice(0, len) + '...' : text
}

function readMore(htmlFile) {
  window.location.href = baseUrl + htmlFile
}
</script>

<template>
  <article class="article-card">
    <!-- 縮圖 -->
    <div class="card-thumbnail">
      <img
        v-if="article.thumbnail && !article.thumbnail.includes('placeholder')"
        :src="baseUrl + article.thumbnail"
        :alt="article.title"
      />
      <div v-else class="thumbnail-placeholder">
        <svg width="40" height="40" viewBox="0 0 40 40" fill="none">
          <rect x="4" y="8" width="32" height="24" rx="2" stroke="#ccc" stroke-width="1.5" fill="none"/>
          <circle cx="14" cy="17" r="4" stroke="#ccc" stroke-width="1.5" fill="none"/>
          <path d="M4 28 L12 20 L20 26 L28 18 L36 26" stroke="#ccc" stroke-width="1.5" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </div>
    </div>

    <!-- 文章資訊 -->
    <div class="card-body">
      <h2 class="card-title">{{ article.title }}</h2>
      <p class="card-excerpt">{{ truncate(article.content) }}</p>
    </div>

    <!-- 右側：日期 + Read More -->
    <div class="card-meta">
      <span class="card-date">{{ formatDate(article.date) }}</span>
      <button class="read-more-btn" @click="readMore(article.htmlFile)">
        Read More
      </button>
    </div>
  </article>
</template>

<style scoped>
.article-card {
  display: flex;
  align-items: stretch;
  gap: 1.5rem;
  padding: 1.75rem 0;
  border-bottom: 1px solid #e8e8e8;
}
.article-card:last-child {
  border-bottom: none;
}

.card-thumbnail {
  flex-shrink: 0;
  width: 140px;
  height: 105px;
  border-radius: 6px;
  overflow: hidden;
  background: #f0f0f0;
}
.card-thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.thumbnail-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f0f0f0;
}

.card-body {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.6rem;
  min-width: 0;
}
.card-title {
  font-size: 1.05rem;
  font-weight: 700;
  color: #222;
  line-height: 1.4;
  margin: 0;
}
.card-excerpt {
  font-size: 0.875rem;
  color: #777;
  line-height: 1.7;
  margin: 0;
}

.card-meta {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: space-between;
  flex-shrink: 0;
  min-width: 100px;
  padding-top: 2px;
}
.card-date {
  font-size: 0.8rem;
  color: #aaa;
  white-space: nowrap;
}
.read-more-btn {
  background: none;
  border: 1.5px solid #C8342A;
  color: #C8342A;
  font-family: 'Microsoft JhengHei', '微軟正黑體', sans-serif;
  font-size: 0.8rem;
  padding: 5px 14px;
  border-radius: 4px;
  cursor: pointer;
  transition: background 0.15s, color 0.15s;
  white-space: nowrap;
}
.read-more-btn:hover {
  background: #C8342A;
  color: #fff;
}

@media (max-width: 600px) {
  .article-card {
    flex-wrap: wrap;
  }
  .card-thumbnail {
    width: 100px;
    height: 80px;
  }
  .card-meta {
    flex-direction: row;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    padding-top: 0;
  }
}
</style>
