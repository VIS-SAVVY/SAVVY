<template>
  <section id="teaser" class="section-dark sec-pad">
    <div class="teaser-inner">
      <h2 class="sec-title">Teaser</h2>
      <div class="divider"></div>
      <img
        src="/images/teaser.jpg"
        alt="Teaser: Overview of the SAVVY system"
        class="teaser-img"
      />
    </div>
  </section>
</template>

<style scoped>
.teaser-inner {
  max-width: 1100px;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
  padding-left: clamp(16px, 4vw, 40px);
  padding-right: clamp(16px, 4vw, 40px);
}
.sec-title {
  font-family: Arial, sans-serif;
  font-size: 28.8px;
  font-weight: 700;
  color: var(--text);
  text-align: center;
  margin-bottom: 12px;
}
.teaser-img {
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 4px 24px rgba(0,0,0,.35);
}
</style>
