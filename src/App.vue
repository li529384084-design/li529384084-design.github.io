<template>
  <main class="site-shell">
    <div class="mesh mesh-one" />
    <div class="mesh mesh-two" />
    <div class="mesh mesh-three" />

    <nav class="nav">
      <a class="brand" href="#top"><span class="brand-mark">J</span><span>Jacklin</span></a>
      <div class="nav-links">
        <a href="#about">关于我</a>
        <a href="#resources">资源</a>
        <a class="nav-contact" href="https://t.me/dazhao668" target="_blank">联系我</a>
      </div>
    </nav>

    <section id="top" class="hero">
      <div class="eyebrow"><span class="status-dot" />探索、创造、持续成长</div>
      <h1>用好奇心创造<span>有温度的数字体验。</span></h1>
      <p class="hero-copy">
        你好，我是 Jacklin。这里记录我的技术探索、灵感与生活，也分享值得收藏的数字资源。
      </p>
      <div class="hero-actions">
        <a class="button button-primary" href="https://t.me/dazhao668" target="_blank">
          Telegram 联系我 <span>↗</span>
        </a>
        <a class="button button-secondary" href="#resources">查看分享 <span>↓</span></a>
      </div>
      <div class="hero-visual">
        <div class="orb orb-main">
          <span class="orb-letter">J</span>
          <div class="orbit orbit-one" />
          <div class="orbit orbit-two" />
        </div>
        <div class="floating-chip chip-one">Ideas</div>
        <div class="floating-chip chip-two">Create</div>
        <div class="floating-chip chip-three">Share</div>
      </div>
    </section>

    <section id="about" class="section">
      <div class="section-heading">
        <span>ABOUT</span>
        <h2>简单、专注，也保持想象力。</h2>
        <p>我相信好的体验应当自然、清晰，并让复杂的事情变得容易理解。</p>
      </div>
      <div class="feature-grid">
        <article class="feature-card feature-large">
          <div class="card-icon">✦</div>
          <div>
            <span class="card-label">持续创造</span>
            <h3>把灵感变成真实可用的作品。</h3>
            <p>关注技术与设计，用持续迭代让每一个想法更完整。</p>
          </div>
        </article>
        <article class="feature-card">
          <div class="mini-orb" />
          <div>
            <span class="card-label">个人主页</span>
            <h3>Jacklin's Space</h3>
            <a href="https://github.com/li529384084-design" target="_blank">访问 GitHub ↗</a>
          </div>
        </article>
        <article class="feature-card dark-card">
          <div class="sparkles">✦　·　✧</div>
          <div>
            <span class="card-label">保持联系</span>
            <h3>@dazhao668</h3>
            <a href="https://t.me/dazhao668" target="_blank">在 Telegram 联系我 ↗</a>
          </div>
        </article>
      </div>
    </section>

    <section id="resources" class="section resource-section">
      <div class="resource-copy">
        <span class="section-kicker">SHARED RESOURCE</span>
        <h2>我的夸克网盘分享</h2>
        <p>我用夸克网盘给你分享了「来自：分享」。点击下方按钮，即可打开夸克网盘获取内容。</p>
        <div class="share-code">
          <span>提取口令</span>
          <strong>/~7f583Z0C8u~:/</strong>
          <button type="button" @click="copyShareCode">{{ copied ? "已复制" : "复制" }}</button>
        </div>
        <a class="button button-primary" href="https://pan.quark.cn/s/98f9669a70be" target="_blank">
          打开夸克网盘 <span>↗</span>
        </a>
      </div>
      <a class="resource-card" href="https://pan.quark.cn/s/98f9669a70be" target="_blank">
        <div class="resource-glow" />
        <div class="folder">
          <div class="folder-tab" />
          <div class="folder-body"><span>Q</span></div>
        </div>
        <div class="resource-meta"><span>QUARK CLOUD</span><strong>来自：分享</strong></div>
      </a>
    </section>

    <footer class="footer">
      <a class="brand" href="#top"><span class="brand-mark">J</span><span>Jacklin</span></a>
      <p>© {{ year }} Jacklin. Keep curious, keep creating.</p>
      <div>
        <a href="https://t.me/dazhao668" target="_blank">Telegram</a>
        <a href="https://github.com/li529384084-design" target="_blank">GitHub</a>
        <a href="https://github.com/imsyy/home" target="_blank">Based on imsyy/home</a>
      </div>
    </footer>
  </main>
</template>

<script setup>
const year = new Date().getFullYear();
const copied = ref(false);

const copyShareCode = async () => {
  await navigator.clipboard.writeText("/~7f583Z0C8u~:/");
  copied.value = true;
  window.setTimeout(() => (copied.value = false), 1800);
};
</script>
