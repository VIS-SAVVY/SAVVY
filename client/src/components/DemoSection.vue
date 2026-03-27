<template>
  <section id="demo" class="section-dark sec-pad">
    <div class="inner">
      <h2 class="sec-title">Demo Application</h2>
      <div class="divider"></div>
      <div class="demo-wrap ph-box">
        <span class="ph-icon">🖥</span>
        <p class="ph-label">Interactive Demo</p>
        <p class="ph-hint">Online demo link or embedded interactive application will be placed here.</p>
        <a href="#" class="btn-demo disabled" title="Demo coming soon">Try Demo (Coming Soon)</a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.sec-title {
  font-family: Arial, sans-serif;
  font-size: 28.8px;
  font-weight: 700;
  color: var(--text);
  text-align: center;
  margin-bottom: 12px;
}
.demo-wrap {
  max-width: 580px;
  margin: 0 auto;
  padding: clamp(36px, 7vw, 56px) clamp(16px, 4vw, 24px);
  flex-direction: column;
  gap: 12px;
}
.ph-icon  { font-size: clamp(1.8rem, 4vw, 2.4rem); opacity: .55; }
.ph-label { font-size: clamp(0.85rem, 2vw, 0.95rem); font-weight: 600; color: var(--muted); }
.ph-hint  { font-size: clamp(0.78rem, 1.8vw, 0.85rem); color: var(--muted); max-width: 340px; line-height: 1.5; text-align: center; }
.btn-demo {
  display: inline-block;
  margin-top: 8px;
  padding: 10px 28px;
  background: var(--accent);
  color: #052e16;
  border-radius: 999px;
  font-weight: 600;
  font-size: clamp(0.82rem, 2vw, 0.9rem);
  text-decoration: none;
  transition: background .2s;
}
.btn-demo:hover { background: #22c55e; }
.btn-demo.disabled { opacity: .4; pointer-events: none; cursor: not-allowed; }
</style>
