<template>
  <section id="community" class="section community-section">
    <div class="section-heading">
      <span>COMMUNITY</span>
      <h2>留言板与访问记录</h2>
      <p>公开讨论长期保存在 GitHub Issues；下方快捷留言与访问记录仅保存在你的当前浏览器，不上传个人信息。</p>
    </div>

    <div class="stats-grid">
      <article><span>本站总访问</span><strong id="busuanzi_value_site_pv">--</strong><small>匿名页面浏览量</small></article>
      <article><span>本站访客</span><strong id="busuanzi_value_site_uv">--</strong><small>匿名访客估算</small></article>
      <article><span>今日访问</span><strong>{{ todayVisits }}</strong><small>当前浏览器</small></article>
      <article><span>最近访问</span><strong>{{ lastVisit }}</strong><small>当前浏览器</small></article>
    </div>

    <div class="community-grid">
      <div class="guestbook-card">
        <div class="community-card-heading">
          <div><span class="tech-label">LOCAL GUESTBOOK</span><h3>快捷留言</h3></div>
          <button type="button" @click="clearMessages">清空本机留言</button>
        </div>
        <form class="message-form" @submit.prevent="addMessage">
          <input v-model.trim="name" maxlength="20" placeholder="你的称呼" required />
          <textarea v-model.trim="content" maxlength="280" placeholder="想说点什么？" required />
          <button class="button button-primary" type="submit">留下留言</button>
        </form>
        <div class="message-list">
          <article v-for="message in messages" :key="message.id" class="message-item">
            <div><strong>{{ message.name }}</strong><time>{{ message.time }}</time></div>
            <p>{{ message.content }}</p>
            <button type="button" @click="replyTo = message.id">回复</button>
            <form v-if="replyTo === message.id" class="reply-form" @submit.prevent="addReply(message)">
              <input v-model.trim="replyContent" maxlength="180" placeholder="写下回复" required />
              <button type="submit">发送</button>
            </form>
            <p v-for="reply in message.replies" :key="reply.id" class="reply-item"><strong>回复：</strong>{{ reply.content }}</p>
          </article>
          <p v-if="messages.length === 0" class="empty-state">还没有本机留言，来坐第一排。</p>
        </div>
      </div>

      <aside class="visitor-card">
        <span class="tech-label">PUBLIC DISCUSSION</span>
        <h3>公开留言与回复</h3>
        <p>登录 GitHub 后，可以发布永久公开留言、回复其他访客，并接收回复通知。</p>
        <a class="button button-primary" href="https://github.com/li529384084-design/li529384084-design.github.io/issues/new?title=Guestbook%3A%20" target="_blank" rel="noreferrer">发布公开留言 ↗</a>
        <div class="visit-log">
          <strong>本机最近访问记录</strong>
          <time v-for="visit in recentVisits" :key="visit">{{ visit }}</time>
        </div>
      </aside>
    </div>
  </section>
</template>

<script setup>
const STORAGE_KEY = "jacklin-guestbook";
const VISIT_KEY = "jacklin-visits";
const name = ref("");
const content = ref("");
const replyContent = ref("");
const replyTo = ref(null);
const messages = ref([]);
const recentVisits = ref([]);
const todayVisits = computed(() => {
  const today = new Date().toLocaleDateString("zh-CN");
  return recentVisits.value.filter((visit) => visit.startsWith(today)).length;
});
const lastVisit = computed(() => recentVisits.value[1]?.split(" ")[1] || "首次");

const persistMessages = () => localStorage.setItem(STORAGE_KEY, JSON.stringify(messages.value));
const addMessage = () => {
  messages.value.unshift({ id: Date.now(), name: name.value, content: content.value, time: new Date().toLocaleString("zh-CN"), replies: [] });
  content.value = "";
  persistMessages();
};
const addReply = (message) => {
  message.replies.push({ id: Date.now(), content: replyContent.value });
  replyContent.value = "";
  replyTo.value = null;
  persistMessages();
};
const clearMessages = () => {
  messages.value = [];
  persistMessages();
};

onMounted(() => {
  messages.value = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
  const visits = JSON.parse(localStorage.getItem(VISIT_KEY) || "[]");
  visits.unshift(new Date().toLocaleString("zh-CN"));
  recentVisits.value = visits.slice(0, 6);
  localStorage.setItem(VISIT_KEY, JSON.stringify(recentVisits.value));

  if (!document.querySelector('script[data-stats="busuanzi"]')) {
    const script = document.createElement("script");
    script.src = "https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js";
    script.async = true;
    script.dataset.stats = "busuanzi";
    document.body.appendChild(script);
  }
});
</script>
