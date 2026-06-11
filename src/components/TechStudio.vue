<template>
  <section id="tech" class="section tech-section">
    <div class="section-heading">
      <span>TECH STUDIO</span>
      <h2>技术播客与实践手册</h2>
      <p>把踩坑、配置、工具和代码沉淀成可以复用的经验。</p>
    </div>

    <div class="podcast-card">
      <div class="podcast-cover"><span>J</span><small>TECH RADIO</small></div>
      <div class="podcast-copy">
        <span class="tech-label">JACKLIN TECH RADIO · 筹备中</span>
        <h3>聊真实开发，也聊那些文档没有写清楚的事。</h3>
        <p>计划分享独立开发、开源项目、效率工具和报错排查。首期上线后，可在这里直接收听。</p>
        <a class="button button-primary" href="https://t.me/dazhao668" target="_blank" rel="noreferrer">投稿选题 ↗</a>
      </div>
      <div class="sound-bars" aria-hidden="true"><i v-for="bar in 18" :key="bar" /></div>
    </div>

    <div class="tech-grid">
      <article v-for="item in techColumns" :key="item.title" class="tech-card">
        <span class="tech-icon">{{ item.icon }}</span>
        <span class="tech-label">{{ item.label }}</span>
        <h3>{{ item.title }}</h3>
        <p>{{ item.description }}</p>
        <ul><li v-for="entry in item.items" :key="entry">{{ entry }}</li></ul>
      </article>
    </div>

    <div class="code-showcase">
      <div class="code-copy">
        <span class="tech-label">CODE HIGHLIGHT</span>
        <h3>命令脚本仓库</h3>
        <p>用一条脚本完成项目体检：安装依赖、构建，并检查未提交的变更。</p>
        <a href="https://github.com/li529384084-design" target="_blank" rel="noreferrer">查看我的 GitHub ↗</a>
      </div>
      <div class="code-window">
        <div class="code-toolbar"><span /><span /><span /><strong>project-check.sh</strong></div>
        <pre><code><span class="code-comment">#!/usr/bin/env bash</span>
<span class="code-keyword">set</span> -euo pipefail

<span class="code-command">corepack pnpm</span> install
<span class="code-command">corepack pnpm</span> build

<span class="code-keyword">if</span> ! git diff --quiet; <span class="code-keyword">then</span>
  <span class="code-command">git</span> status --short
  <span class="code-keyword">exit</span> 1
<span class="code-keyword">fi</span>

<span class="code-string">echo "Project check passed."</span></code></pre>
      </div>
    </div>
  </section>
</template>

<script setup>
const techColumns = [
  { icon: "✓", label: "ENVIRONMENT", title: "环境配置清单", description: "新设备从零开始的开发环境核对表。", items: ["Node.js 与 Corepack", "Git 与 SSH 密钥", "VS Code 常用扩展", "环境变量与密钥隔离"] },
  { icon: "!", label: "DEBUG LOG", title: "报错排查记录", description: "记录现象、原因、验证过程和最终修复。", items: ["复现条件与错误日志", "最小可复现示例", "根因与错误假设", "回归测试结果"] },
  { icon: "↗", label: "OPEN SOURCE", title: "开源项目演示", description: "展示项目动机、技术架构与在线效果。", items: ["在线 Demo 与源码", "核心功能拆解", "架构决策记录", "版本路线图"] },
  { icon: "★", label: "TOOL REVIEW", title: "工具测评", description: "从真实使用场景出发，不只罗列参数。", items: ["适合谁与不适合谁", "学习与迁移成本", "优缺点和替代方案", "长期使用结论"] },
];
</script>
