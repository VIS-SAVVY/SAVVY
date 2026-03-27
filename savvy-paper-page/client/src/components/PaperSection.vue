<template>
  <section id="paper" class="section-dark sec-pad">
    <div class="inner">
      <h2 class="sec-title">Paper</h2>
      <div class="divider"></div>

      <div class="paper-card">
        <div class="ph-box thumb-ph">
          <span class="ph-icon">📄</span>
          <p class="ph-label">Paper Thumbnail</p>
        </div>

        <div class="paper-info">
          <h3 class="paper-name">SAVVY: Student Attention Visualization for Video-based Learning Analysis</h3>
          <p class="paper-authors">Author One, Author Two, Author Three, Author Four</p>
          <p class="paper-venue"><em>Conference / Journal Name</em>, 2026</p>

          <div class="paper-links">
            <a v-for="btn in paperBtns" :key="btn.label"
               href="#" class="btn-paper disabled" :title="btn.title">
              {{ btn.icon }} {{ btn.label }}
            </a>
          </div>

          <div class="bibtex-wrap">
            <p class="bibtex-heading">BibTeX</p>
            <pre class="code-block">{{ bibtex }}</pre>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const paperBtns = [
  { icon: "📄", label: "PDF (Coming Soon)",   title: "PDF coming soon" },
  { icon: "🔗", label: "arXiv (Coming Soon)", title: "arXiv coming soon" },
  { icon: "💻", label: "Code (Coming Soon)",  title: "Code coming soon" },
]
const bibtex = `@inproceedings{savvy2026,
  title     = {SAVVY: Student Attention Visualization for Video-based Learning Analysis},
  author    = {Author One and Author Two and Author Three and Author Four},
  booktitle = {Conference/Journal Name},
  year      = {2026},
  <!-- [fill in pages, doi, url, etc.] -->
}`
</script>

<style scoped>
.sec-title {
  font-family: Arial, sans-serif;
  font-size: 28.8px;
  font-weight: 700;
  color: var(--text);
  text-align: center;
  margin-bottom: 12px;
}
.paper-card {
  display: flex;
  gap: clamp(20px, 4vw, 36px);
  align-items: flex-start;
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: clamp(20px, 4vw, 36px) clamp(16px, 4vw, 40px);
  flex-wrap: wrap;
  backdrop-filter: blur(6px);
}
.thumb-ph {
  width: clamp(120px, 18vw, 180px);
  min-height: clamp(160px, 24vw, 240px);
  flex-shrink: 0;
}
.ph-icon  { font-size: clamp(1.6rem, 3vw, 2rem); opacity: .55; }
.ph-label { font-size: clamp(0.75rem, 1.7vw, 0.82rem); font-weight: 600; color: var(--muted); margin-top: 8px; }
.paper-info { flex: 1; min-width: 240px; }
.paper-name {
  font-size: clamp(0.95rem, 2.2vw, 1.15rem);
  font-weight: 700;
  color: var(--text);
  margin-bottom: 8px;
  line-height: 1.4;
}
.paper-authors { font-size: clamp(0.80rem, 1.8vw, 0.88rem); color: var(--muted); margin-bottom: 6px; }
.paper-venue   { font-size: clamp(0.80rem, 1.8vw, 0.88rem); color: var(--accent); margin-bottom: 18px; }
.paper-venue em { font-style: italic; }
.paper-links { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 22px; }
.btn-paper {
  display: inline-block;
  padding: 7px 14px;
  background: rgba(255,255,255,0.07);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 6px;
  font-size: clamp(0.78rem, 1.8vw, 0.85rem);
  font-weight: 500;
  text-decoration: none;
  transition: all .2s;
  white-space: nowrap;
}
.btn-paper:hover { border-color: var(--accent); color: var(--accent); }
.btn-paper.disabled { opacity: .4; pointer-events: none; cursor: not-allowed; }
.bibtex-heading { font-size: clamp(0.80rem, 1.8vw, 0.88rem); font-weight: 600; color: var(--muted); margin-bottom: 8px; }
@media (max-width: 520px) {
  .paper-card { flex-direction: column; align-items: center; }
  .thumb-ph { width: 120px; min-height: 160px; }
  .paper-info { min-width: unset; width: 100%; }
}
</style>
