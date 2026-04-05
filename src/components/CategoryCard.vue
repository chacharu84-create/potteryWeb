<script setup>
defineProps({
  category: {
    type: Object,
    required: true,
  },
})

const baseUrl = import.meta.env.BASE_URL
</script>

<template>
  <div class="cat-card">
    <div class="cat-icon">
      <img
        v-if="category.iconUrl"
        :src="baseUrl + category.iconUrl"
        :alt="category.name"
        class="cat-icon-img"
      />
    </div>
    <h3 class="cat-name">{{ category.name }}</h3>
    <p class="cat-desc">{{ category.description }}</p>
  </div>
</template>

<style scoped>
.cat-card {
  background: #fff;
  border-radius: 8px;
  padding: 2.5rem 2rem 2rem;
  text-align: center;
  box-shadow: 0 2px 12px rgba(0,0,0,0.06);
  transition: box-shadow 0.2s, transform 0.2s;
  cursor: default;
  height: 100%;
}
.cat-card:hover {
  box-shadow: 0 6px 24px rgba(0,0,0,0.1);
  transform: translateY(-2px);
}
.cat-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 88px;
  margin-bottom: 1.2rem;
}
.cat-icon-img {
  width: 88px;
  height: 88px;
  object-fit: contain;
}
.cat-name {
  font-size: 1.15rem;
  font-weight: 700;
  color: #333;
  margin-bottom: 0.75rem;
}
.cat-desc {
  font-size: 0.85rem;
  color: #888;
  line-height: 1.7;
}
</style>
