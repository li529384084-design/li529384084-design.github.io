<template>
  <main class="site-shell">
    <MeteorCursor />
    <div class="mesh mesh-one" /><div class="mesh mesh-two" /><div class="mesh mesh-three" />
    <nav class="nav">
      <a class="brand" href="#top"><span class="brand-mark">J</span><span>Jacklin</span></a>
      <div class="nav-links">
        <a href="#tech">技术</a><a href="#story">故事</a><a href="#resources">资源</a><a href="#community">留言</a>
        <a class="nav-contact" href="https://t.me/dazhao668" target="_blank" rel="noreferrer">联系我</a>
      </div>
    </nav>

    <section id="top" class="hero">
      <div class="eyebrow"><span class="status-dot" />探索、创造、持续成长</div>
      <h1>用好奇心创造<span>有温度的数字体验。</span></h1>
      <p class="hero-copy">你好，我是 Jacklin。这里记录我的技术探索、灵感与生活，也分享值得收藏的合法免费资源。</p>
      <div class="hero-actions">
        <a class="button button-primary" href="#story">阅读故事 <span>↓</span></a>
        <a class="button button-secondary" href="#resources">浏览资源 <span>↗</span></a>
      </div>
      <div class="hero-visual">
        <div class="orb orb-main"><span class="orb-letter">J</span><div class="orbit orbit-one" /><div class="orbit orbit-two" /></div>
        <div class="floating-chip chip-one">Ideas</div><div class="floating-chip chip-two">Create</div><div class="floating-chip chip-three">Share</div>
      </div>
    </section>

    <section id="about" class="section">
      <div class="section-heading"><span>ABOUT</span><h2>简单、专注，也保持想象力。</h2><p>我相信好的体验应当自然、清晰，并让复杂的事情变得容易理解。</p></div>
      <div class="feature-grid">
        <article class="feature-card feature-large"><div class="card-icon">✦</div><div><span class="card-label">持续创造</span><h3>把灵感变成真实可用的作品。</h3><p>关注技术与设计，用持续迭代让每一个想法更完整。</p></div></article>
        <article class="feature-card"><div class="mini-orb" /><div><span class="card-label">个人主页</span><h3>Jacklin's Space</h3><a href="https://github.com/li529384084-design" target="_blank" rel="noreferrer">访问 GitHub ↗</a></div></article>
        <article class="feature-card dark-card"><div class="sparkles">✦　·　✧</div><div><span class="card-label">保持联系</span><h3>@dazhao668</h3><a href="https://t.me/dazhao668" target="_blank" rel="noreferrer">在 Telegram 联系我 ↗</a></div></article>
      </div>
    </section>

    <TechStudio />

    <section id="story" class="section story-section">
      <div class="section-heading"><span>STORY</span><h2>把人生活成一篇励志文</h2><p>关于自律、逃避，以及一个写得比做得漂亮的人。</p></div>
      <article class="story-card">
        <div class="story-meta"><span>Jacklin</span><span>随笔 · 约 5 分钟阅读</span></div>
        <div class="story-body"><p v-for="(paragraph, index) in storyParagraphs" :key="index" :class="{ 'story-turn': paragraph === '等等。' }">{{ paragraph }}</p></div>
      </article>
    </section>

    <section id="safety" class="section safety-section">
      <div class="section-heading"><span>SAFETY GUIDE</span><h2>破解网站避雷指南</h2><p>不提供破解网站入口。记住这些信号，能更有效地避开恶意下载、账号盗取和隐私泄露。</p></div>
      <div class="warning-grid">
        <article v-for="warning in warnings" :key="warning.title" class="warning-card"><span>{{ warning.number }}</span><h3>{{ warning.title }}</h3><p>{{ warning.description }}</p></article>
      </div>
      <div class="safety-note"><strong>发现可疑网站时</strong><p>不要下载或运行文件，不要关闭安全软件，不要输入账号、密码或验证码。关闭页面后清理下载内容，并通过浏览器举报功能或国家反诈中心渠道反馈。</p></div>
    </section>

    <section id="resources" class="section resources-section">
      <div class="resources-header">
        <div class="section-heading"><span>LEGAL & FREE</span><h2>合法免费资源导航</h2><p>收录 {{ resourceLinks.length }} 个合法、免费、开源或公共领域资源。部分服务含付费增值内容，请以网站说明为准。</p></div>
        <label class="resource-search"><span>搜索</span><input v-model.trim="resourceQuery" type="search" placeholder="搜索名称或分类…" /></label>
      </div>
      <div class="category-filters" aria-label="资源分类">
        <button v-for="category in categories" :key="category" type="button" :class="{ active: activeCategory === category }" @click="activeCategory = category">{{ category }}</button>
      </div>
      <div class="resource-grid">
        <a v-for="resource in filteredResources" :key="resource.url" class="resource-link-card" :href="resource.url" target="_blank" rel="noreferrer">
          <span class="resource-category">{{ resource.category }}</span><strong>{{ resource.name }}</strong><span class="resource-arrow">↗</span>
        </a>
      </div>
      <div v-if="filteredResources.length === 0" class="empty-state">没有找到匹配的资源，换个关键词试试。</div>
    </section>

    <CommunityBoard />

    <footer class="footer">
      <a class="brand" href="#top"><span class="brand-mark">J</span><span>Jacklin</span></a><p>© {{ year }} Jacklin. Keep curious, keep creating.</p>
      <div><a href="https://t.me/dazhao668" target="_blank" rel="noreferrer">Telegram</a><a href="https://github.com/li529384084-design" target="_blank" rel="noreferrer">GitHub</a><a href="https://github.com/imsyy/home" target="_blank" rel="noreferrer">Based on imsyy/home</a></div>
    </footer>
  </main>
</template>

<script setup>
import resourceLinks from "@/assets/resourceLinks.js";

const year = new Date().getFullYear();
const resourceQuery = ref("");
const activeCategory = ref("全部");
const categories = ["全部", ...new Set(resourceLinks.map((resource) => resource.category))];
const filteredResources = computed(() => {
  const query = resourceQuery.value.toLowerCase();
  return resourceLinks.filter((resource) => {
    const matchesCategory = activeCategory.value === "全部" || resource.category === activeCategory.value;
    const matchesQuery = !query || `${resource.name} ${resource.category}`.toLowerCase().includes(query);
    return matchesCategory && matchesQuery;
  });
});

const warnings = [
  { number: "01", title: "要求关闭安全软件", description: "任何要求停用杀毒软件、防火墙或系统保护的下载说明，都应立即停止操作。" },
  { number: "02", title: "捆绑补丁与激活器", description: "所谓破解补丁、注册机和激活器常被用来夹带木马、勒索软件或挖矿程序。" },
  { number: "03", title: "强制跳转与密集弹窗", description: "连续跳转、虚假下载按钮和成人或博彩广告，通常意味着网站缺乏可信管理。" },
  { number: "04", title: "索取敏感信息", description: "下载前要求账号密码、验证码、支付信息或安装描述文件，可能是在窃取身份。" },
  { number: "05", title: "文件与说明不符", description: "扩展名异常、压缩包多重加密、文件体积反常，都是应立即删除的危险信号。" },
  { number: "06", title: "没有授权与来源说明", description: "宣称永久破解、永久免费，却无法说明作者、许可证和原始来源，通常不可信。" },
];

const storyParagraphs = [
  "凌晨四点，我又一次被闹钟从噩梦中拽出来。",
  "这是我裸辞的第三百天。卡里的存款从六位数熬成了三位数，投出去的简历像石沉大海，连面试邀请都懒得再给我发一封。",
  "但我没有放弃。",
  "我把出租屋的墙贴满了便利贴，上面写满了每天的目标：早起跑步五公里、背两百个单词、精读一本行业书、复盘一次失败经历。我逼自己活得像个精密运转的机器，不敢有一丝懈怠。朋友劝我歇一歇，我说：\"不行，我还不够好。\"",
  "三百天里，我瘦了二十斤，黑眼圈重到同事以为我得了什么大病。我终于拿到了那家顶级公司的 offer，入职那天，HR 对我说：\"你的自律和韧性，是我们见过最强的。\"",
  "我笑了，笑得眼眶发红。",
  "我以为我终于赢了。",
  "直到三个月后，我在公司厕所里崩溃大哭。",
  "因为我发现，那个在出租屋里咬着牙死撑的自己，不过是在用一种更精致的方式逃避真正的问题——我不敢承认，我根本不喜欢这个行业，我只是害怕停下来之后，发现自己其实一无是处。",
  "我用三百天的\"励志\"，把自己包装成了一个完美的奋斗者，却骗了自己整整一年。",
  "后来我辞了那份别人眼里光鲜的工作，去了一家小公司做自己喜欢的内容策划。工资只有原来的一半，但每天早上醒来，我不再需要靠闹钟把自己从噩梦里拽出来了。",
  "有时候我觉得，真正的励志不是咬牙硬撑到赢，而是终于敢对自己说一句：算了，这条路不适合我。",
  "然后转身，走向另一条没人看好的路。",
  "……",
  "等等。",
  "刚才那段话，是我昨晚花三个小时写的博客草稿。",
  "事实上，我今天早上 10 点才起床，健身计划已经断了两周，书停在第 37 页再没翻过，简历也还在邮箱草稿箱里躺着没发出去。",
  "那些贴在墙上的便利贴？上周大扫除的时候被我撕下来扔垃圾桶了。",
  "至于那家顶级公司的 offer——",
  "哦，那是我编的。",
  "我唯一真实拿到的东西，是这篇还没发出去的文章，和一个依然不知道明天在哪里的自己。",
  "所以你看，连\"触底反弹、认清自我、重新出发\"这种故事，我都写得比做得漂亮。",
  "这大概就是我最擅长的事情吧：把人生活成一篇励志文，然后继续赖在床上。",
];
</script>
