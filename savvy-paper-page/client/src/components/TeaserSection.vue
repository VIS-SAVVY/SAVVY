<template>
  <section id="teaser" class="section-dark sec-pad">
    <div class="inner">
      <div class="ph-box teaser-ph">
        <span class="ph-icon">🖼</span>
        <p class="ph-label">Teaser Image / Screenshot</p>
        <p class="ph-hint">Replace with your paper's teaser figure (e.g., system overview, key results)</p>
      </div>
      <p class="caption">
        Figure 1: Overview of the SAVVY system. (a)&nbsp;… &nbsp;(b)&nbsp;… &nbsp;(c)&nbsp;…
      </p>
    </div>
  </section>
</template>

<style scoped>
.teaser-ph {
  width: 100%;
  height: clamp(200px, 40vw, 420px);
  flex-direction: column;
  gap: 10px;
}
.ph-icon  { font-size: clamp(1.6rem, 4vw, 2.4rem); opacity: .55; }
.ph-label { font-size: clamp(0.82rem, 2vw, 0.95rem); font-weight: 600; color: var(--muted); }
.ph-hint  { font-size: clamp(0.75rem, 1.8vw, 0.82rem); max-width: 300px; line-height: 1.5; opacity: .75; text-align: center; color: var(--muted); }
.caption {
  margin-top: 16px;
  font-size: clamp(0.78rem, 1.8vw, 0.88rem);
  color: var(--muted);
  font-style: italic;
  line-height: 1.6;
  text-align: center;
}
.teaser-img { width: 100%; border-radius: 12px; box-shadow: 0 4px 24px rgba(0,0,0,.35); }
</style>
