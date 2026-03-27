<template>
  <section id="video" class="section-dark sec-pad">
    <div class="inner">
      <h2 class="sec-title">Video</h2>
      <div class="divider"></div>

      <!-- 主视频占位 — 替换为 <video> 或 YouTube <iframe> -->
      <div class="video-wrap">
        <div class="ph-box video-ph">
          <span class="ph-icon">▶</span>
          <p class="ph-label">Main Demo Video</p>
          <p class="ph-hint">Replace with &lt;video&gt; or YouTube &lt;iframe&gt;</p>
        </div>
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
.divider {
  width: 52px; height: 3px;
  background: var(--accent);
  border-radius: 2px;
  margin: 0 auto 2.5rem;
}
.video-wrap {
  width: 100%;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 32px rgba(0,0,0,.4);
  border: 1px solid var(--border);
}
.video-ph {
  width: 100%;
  aspect-ratio: 16/9;
  background: rgba(255,255,255,0.07);
  flex-direction: column;
  gap: 10px;
  border-radius: 0;
  border: none;
}
.ph-icon  { font-size: clamp(2rem, 5vw, 3rem); opacity: .4; }
.ph-label { font-size: clamp(0.85rem, 2vw, 1rem); font-weight: 600; color: var(--muted); }
.ph-hint  { font-size: clamp(0.75rem, 1.8vw, 0.85rem); color: var(--muted); text-align: center; opacity: .75; }
</style>
