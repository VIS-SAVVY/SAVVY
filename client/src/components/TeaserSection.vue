<template>
  <section id="teaser" class="section-dark sec-pad">
    <div class="teaser-inner">
      <img
        src="/images/teaser.jpg"
        alt="Teaser: Overview of the SAVVY system"
        class="teaser-img"
      />
      <p class="caption">
        Figure 1: Overview of the SAVVY system. (a)&nbsp;… &nbsp;(b)&nbsp;… &nbsp;(c)&nbsp;…
      </p>
    </div>
  </section>
</template>

<style scoped>
/* Teaser inner wrapper matches hero card width exactly */
.teaser-inner {
  max-width: 1100px;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
  padding-left: clamp(16px, 4vw, 40px);
  padding-right: clamp(16px, 4vw, 40px);
}
.teaser-img {
  width: 100%;
  display: block;
  border-radius: 12px;
  box-shadow: 0 4px 24px rgba(0,0,0,.35);
}
.caption {
  margin-top: 16px;
  font-size: clamp(0.78rem, 1.8vw, 0.88rem);
  color: var(--muted);
  font-style: italic;
  line-height: 1.6;
  text-align: center;
}
</style>
