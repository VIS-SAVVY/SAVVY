<template>
  <section id="references" class="section-dark sec-pad">
    <div class="inner">
      <div class="ref-card">
        <h2 class="ref-title">References</h2>
        <ol class="ref-list">
          <li v-for="ref in references" :key="ref.id">
            <span class="ref-num">[{{ ref.id }}]</span>
            <span class="ref-text" v-html="ref.text"></span>
          </li>
        </ol>
      </div>
    </div>
  </section>
</template>

<script setup>
const references = [
  { id: 1, text: 'Z. Zhou, L. Ye, L. Cai, L. Wang, Y. Wang, Y. Wang, W. Chen, and Y. Wang. ConceptThread: Visualizing Threaded Concepts in MOOC Videos. <em>IEEE Transactions on Visualization and Computer Graphics</em>, 31(2):1354–1370, 2024.' },
  { id: 2, text: 'J. T. Fisher, J. R. Keene, R. Huskey, and R. Weber. The Limited Capacity Model of Motivated Mediated Message Processing: Taking Stock of the Past. <em>Annals of the International Communication Association</em>, 42(4):270–290, 2018.' },
  { id: 3, text: 'R. Rosenholtz, Y. Li, and L. Nakano. Measuring Visual Clutter. <em>Journal of Vision</em>, 7(2):17, 2007.' },
  { id: 4, text: 'S. Ceri, A. Bozzon, M. Brambilla, E. Della Valle, P. Fraternali, and S. Quarteroni. An Introduction to Information Retrieval. In <em>Web Information Retrieval</em>, pp. 3–11. Springer, 2013.' },
  { id: 5, text: 'C. E. Shannon. A Mathematical Theory of Communication. <em>The Bell System Technical Journal</em>, 27(3):379–423, 1948.' },
]
</script>

<style scoped>
.ref-card {
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: clamp(24px, 5vw, 40px) clamp(16px, 5vw, 48px);
  backdrop-filter: blur(6px);
}
.ref-title {
  font-family: Arial, sans-serif;
  font-size: 28.8px;
  font-weight: 700;
  color: var(--accent);
  text-align: center;
  margin-bottom: 24px;
}
.ref-list { list-style: none; padding: 0; }
.ref-list li {
  display: grid;
  grid-template-columns: 40px 1fr;
  gap: 0 8px;
  font-family: Arial, sans-serif;
  font-size: 16px;
  color: var(--muted);
  line-height: 1.65;
  padding: 10px 0;
  border-bottom: 1px solid var(--border);
}
.ref-list li:last-child { border-bottom: none; }
.ref-num { font-family: Arial, sans-serif; color: var(--accent); font-weight: 600; font-size: 16px; padding-top: 2px; }
.ref-text :deep(em) { color: var(--text); font-style: italic; }
</style>
