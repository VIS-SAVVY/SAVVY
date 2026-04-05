<template>
  <section class="hero-wrap">
    <!-- Card 1: title + nav buttons -->
    <div class="hero-card">
      <h1 class="paper-title">
        SAVVY: Student Attention Visualization for Video-based Learning Analysis
      </h1>
      <nav class="hero-nav">
        <a v-for="link in navLinks" :key="link.href" :href="link.href" class="nav-link">
          {{ link.label }}
        </a>
      </nav>
    </div>

    <!-- Card 2: paper figure, independent rounded card -->
    <div class="hero-img-card">
      <img
        src="/images/fig2.jpg"
        alt="Paper Figure / System Overview"
        class="hero-fig-img"
      />
    </div>
  </section>
</template>

<script setup>
const navLinks = [
  { href: '#teaser',     label: 'Teaser' },
  { href: '#abstract',   label: 'Abstract' },
  { href: '#video',      label: 'Video' },
  { href: '#dataset',    label: 'Dataset' },
  { href: '#code',       label: 'Code' },
  { href: '#references', label: 'References' },
]
</script>

<style scoped>
/* Outer section: gradient bg, column flex so the two cards stack */
.hero-wrap {
  width: 100%;
  box-sizing: border-box;
  background: linear-gradient(150deg, #13131f 0%, #16213e 55%, #0f3460 100%);
  padding: clamp(32px, 6vw, 60px) clamp(16px, 4vw, 24px) clamp(28px, 5vw, 52px);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
}

/* Card 1: title + nav */
.hero-card {
  background: #ffffff;
  border-radius: 20px;
  padding: clamp(28px, 5vw, 52px) clamp(20px, 6vw, 56px) clamp(24px, 4vw, 44px);
  max-width: 1100px;
  width: 100%;
  text-align: center;
  box-shadow:
    0 4px 24px rgba(0,0,0,.18),
    0 1.5px 0 rgba(0,0,0,.10);
}

.paper-title {
  font-family: Arial, sans-serif;
  font-size: clamp(1.4rem, 3.2vw, 2.2rem);
  font-weight: 700;
  color: #111827;
  line-height: 1.35;
  margin-bottom: 28px;
  white-space: normal;
  word-break: keep-all;
  overflow-wrap: break-word;
}

.hero-nav {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 8px;
}

.nav-link {
  display: inline-block;
  padding: 8px 16px;
  border: 2px solid transparent;
  border-radius: 6px;
  color: #333333;
  background-color: #ffffff;
  font-family: Arial, sans-serif;
  font-size: 16px;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.3s;
  white-space: nowrap;
  position: relative;
  box-shadow:
    0 0 0 1.5px rgba(0,0,0,0.14),
    0 0 8px 3px rgba(0,0,0,0.18),
    0 0 20px 6px rgba(0,0,0,0.10);
}
.nav-link:hover {
  background-color: #ffffff;
  color: #000000;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-color: #42b883;
  transform: translateY(-2px);
}

/* Card 2: paper figure */
.hero-img-card {
  max-width: 1100px;
  width: 100%;
  border-radius: 20px;
  overflow: hidden;
  box-shadow:
    0 4px 24px rgba(0,0,0,.18),
    0 1.5px 0 rgba(0,0,0,.10);
  background: #ffffff;
}

.hero-fig-img {
  width: 100%;
  display: block;
  object-fit: contain;
}

@media (max-width: 480px) {
  .hero-card      { border-radius: 14px; }
  .hero-img-card  { border-radius: 14px; }
}
</style>
