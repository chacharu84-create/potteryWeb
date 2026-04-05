<script setup>
// 聯絡我們頁面 — 靜態佔位內容，用戶可自行編輯
</script>

<template>
  <div class="contact-page">
    <div class="container">
      <h1 class="page-title">聯絡我們</h1>
      <p class="page-subtitle">歡迎與我們聯繫，一起推廣在地製陶文化</p>

      <div class="contact-grid">
        <!-- 聯絡資訊 -->
        <div class="contact-info">
          <div class="info-block">
            <div class="info-icon">
              <svg width="22" height="22" viewBox="0 0 22 22" fill="none">
                <path d="M11 2C7.13 2 4 5.13 4 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7z" stroke="#C8342A" stroke-width="1.5" fill="none"/>
                <circle cx="11" cy="9" r="2.5" stroke="#C8342A" stroke-width="1.5" fill="none"/>
              </svg>
            </div>
            <div>
              <h3>工作室地址</h3>
              <p>台灣台東縣XX鄉XX路123號</p>
            </div>
          </div>

          <div class="info-block">
            <div class="info-icon">
              <svg width="22" height="22" viewBox="0 0 22 22" fill="none">
                <path d="M4 4h14a2 2 0 012 2v10a2 2 0 01-2 2H4a2 2 0 01-2-2V6a2 2 0 012-2z" stroke="#C8342A" stroke-width="1.5" fill="none"/>
                <path d="M2 6l9 7 9-7" stroke="#C8342A" stroke-width="1.5" stroke-linecap="round"/>
              </svg>
            </div>
            <div>
              <h3>電子信箱</h3>
              <p>contact@pottery-example.com</p>
            </div>
          </div>

          <div class="info-block">
            <div class="info-icon">
              <svg width="22" height="22" viewBox="0 0 22 22" fill="none">
                <path d="M5 3h3l1.5 4-2 1.5a11 11 0 005 5l1.5-2 4 1.5V16a2 2 0 01-2 2A16 16 0 013 5a2 2 0 012-2z" stroke="#C8342A" stroke-width="1.5" fill="none" stroke-linejoin="round"/>
              </svg>
            </div>
            <div>
              <h3>聯絡電話</h3>
              <p>+886 09XX-XXX-XXX</p>
            </div>
          </div>

          <div class="info-block">
            <div class="info-icon">
              <svg width="22" height="22" viewBox="0 0 22 22" fill="none">
                <rect x="2" y="2" width="18" height="18" rx="5" stroke="#C8342A" stroke-width="1.5" fill="none"/>
                <circle cx="11" cy="11" r="4" stroke="#C8342A" stroke-width="1.5" fill="none"/>
                <circle cx="16.5" cy="5.5" r="1" fill="#C8342A"/>
              </svg>
            </div>
            <div>
              <h3>Instagram</h3>
              <p>@pottery_example</p>
            </div>
          </div>
        </div>

        <!-- 留言表單（佔位，無後端處理） -->
        <div class="contact-form">
          <h2>留下訊息</h2>
          <form @submit.prevent>
            <div class="form-group">
              <label>姓名</label>
              <input type="text" placeholder="您的姓名" />
            </div>
            <div class="form-group">
              <label>電子信箱</label>
              <input type="email" placeholder="your@email.com" />
            </div>
            <div class="form-group">
              <label>訊息內容</label>
              <textarea rows="5" placeholder="請輸入您的訊息..."></textarea>
            </div>
            <button type="submit" class="submit-btn">送出訊息</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.contact-page {
  padding: 4rem 0 6rem;
  min-height: 80vh;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 0 2rem;
}

.page-title {
  font-size: 2.2rem;
  font-weight: 800;
  color: #222;
  margin-bottom: 0.5rem;
}

.page-subtitle {
  font-size: 0.95rem;
  color: #888;
  margin-bottom: 3rem;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 4rem;
}

/* 聯絡資訊 */
.contact-info {
  display: flex;
  flex-direction: column;
  gap: 1.75rem;
}
.info-block {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}
.info-icon {
  flex-shrink: 0;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: #FDF0EF;
  display: flex;
  align-items: center;
  justify-content: center;
}
.info-block h3 {
  font-size: 0.85rem;
  color: #aaa;
  font-weight: 400;
  margin-bottom: 4px;
}
.info-block p {
  font-size: 0.95rem;
  color: #333;
}

/* 表單 */
.contact-form h2 {
  font-size: 1.3rem;
  font-weight: 700;
  color: #222;
  margin-bottom: 1.5rem;
}
.form-group {
  margin-bottom: 1.2rem;
}
.form-group label {
  display: block;
  font-size: 0.85rem;
  color: #555;
  margin-bottom: 6px;
}
.form-group input,
.form-group textarea {
  width: 100%;
  padding: 10px 14px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-family: 'Microsoft JhengHei', '微軟正黑體', sans-serif;
  font-size: 0.9rem;
  color: #333;
  outline: none;
  transition: border-color 0.15s;
  resize: vertical;
}
.form-group input:focus,
.form-group textarea:focus {
  border-color: #C8342A;
}
.submit-btn {
  background: #C8342A;
  color: #fff;
  border: none;
  padding: 12px 32px;
  border-radius: 6px;
  font-family: 'Microsoft JhengHei', '微軟正黑體', sans-serif;
  font-size: 0.95rem;
  cursor: pointer;
  transition: background 0.15s;
}
.submit-btn:hover {
  background: #a82820;
}

@media (max-width: 768px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }
}
</style>
