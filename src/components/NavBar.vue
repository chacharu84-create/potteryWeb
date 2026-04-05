<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

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
  <nav class="navbar">
    <RouterLink to="/" class="navbar-brand">
      <img :src="baseUrl + 'images/logo.jpg'" class="logo-icon" alt="土手製陶 Logo" />
      <span class="brand-name">土手製陶</span>
    </RouterLink>

    <div class="nav-links">
      <!-- 製陶紀錄 dropdown（Bootstrap driven） -->
      <div class="dropdown">
        <button
          class="nav-link-btn dropdown-toggle"
          type="button"
          data-bs-toggle="dropdown"
          aria-expanded="false"
        >
          製陶紀錄
        </button>
        <ul class="dropdown-menu dropdown-menu-end">
          <li v-for="cat in categories" :key="cat.id">
            <button class="dropdown-item" @click="goToCategory(cat.id)">
              {{ cat.name }}
            </button>
          </li>
        </ul>
      </div>

      <!-- 聯絡我們 -->
      <RouterLink to="/contact" class="nav-link-btn">
        聯絡我們
      </RouterLink>

      <!-- 搜尋圖示（佔位） -->
      <button class="nav-icon-btn" aria-label="搜尋">
        <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
          <circle cx="7.5" cy="7.5" r="5.5" stroke="#555" stroke-width="1.5"/>
          <path d="M12 12 L16 16" stroke="#555" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
      </button>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  height: var(--navbar-height);
  background: #fff;
  border-bottom: 1px solid #e5e5e5;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 2.5rem;
}

.navbar-brand {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  color: #333;
}
.logo-icon {
  width: 36px;
  height: 36px;
  object-fit: contain;
  border-radius: 50%;
}
.brand-name {
  font-size: 1.15rem;
  font-weight: 700;
  letter-spacing: 1px;
  color: #333;
}
.navbar-brand:hover .brand-name {
  color: #C8342A;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.nav-link-btn {
  background: none;
  border: none;
  cursor: pointer;
  font-family: 'Microsoft JhengHei', '微軟正黑體', sans-serif;
  font-size: 0.95rem;
  color: #444;
  padding: 0;
  display: flex;
  align-items: center;
  gap: 4px;
  transition: color 0.2s;
  text-decoration: none;
}
.nav-link-btn:hover,
.nav-link-btn.active {
  color: #C8342A;
}

/* Bootstrap dropdown-toggle 的箭頭與 focus outline 覆寫 */
.nav-link-btn.dropdown-toggle::after {
  margin-left: 5px;
  vertical-align: middle;
  border-top-color: currentColor;
}
.nav-link-btn.dropdown-toggle:focus {
  box-shadow: none;
}

/* dropdown-menu 覆寫 */
:deep(.dropdown-menu) {
  border: 1px solid #e5e5e5;
  border-radius: 6px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  min-width: 120px;
  padding: 6px 0;
}

:deep(.dropdown-item) {
  font-family: 'Microsoft JhengHei', '微軟正黑體', sans-serif;
  font-size: 0.9rem;
  color: #444;
  padding: 10px 20px;
  cursor: pointer;
}
:deep(.dropdown-item:hover),
:deep(.dropdown-item:focus) {
  background: #FDF0EF;
  color: #C8342A;
}

.nav-dropdown-wrap {
  position: relative;
}

.chevron {
  transition: transform 0.2s;
}
.chevron.rotated {
  transform: rotate(180deg);
}

.nav-icon-btn {
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #555;
  transition: color 0.2s;
}
.nav-icon-btn:hover {
  color: #C8342A;
}
</style>
