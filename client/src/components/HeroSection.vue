<template>
  <section class="hero-wrap">
    <div class="hero-screen">
      <div class="hero-bg" :style="heroBackgroundStyle" aria-hidden="true"></div>
      <div class="hero-overlay" aria-hidden="true"></div>

      <div class="hero-content">
        <div class="hero-center">
          <div class="logo-stack" :class="{ 'is-revealed': animationStarted }">
            <img
              class="logo logo-vis"
              :src="asset('images/vis2026-logo.svg')"
              alt="IEEE VIS 2026"
            />
          </div>

          <h1
            class="paper-title"
            :class="{ 'is-revealed': animationStarted, 'is-shadow-visible': shadowVisible }"
          >
            <span class="title-line title-line-with-logo">
              <span class="reveal-mask" style="--delay: 1100ms">
                <span class="reveal-segment inline-logo-group">
                  <img
                    class="inline-savvy-logo"
                    :src="asset('images/savvy-system-logo.svg')"
                    alt="SAVVY"
                  />
                  <span class="inline-logo-colon">:</span>
                </span>
              </span>

              <span
                v-for="(word, index) in titleLineOneWords"
                :key="`line-one-${word}-${index}`"
                class="reveal-mask"
                :style="{ '--delay': `${1280 + index * 180}ms` }"
              >
                <span class="reveal-segment title-word">{{ word }}</span>
              </span>
            </span>

            <span class="title-line title-line-two">
              <span
                v-for="(word, index) in titleLineTwoWords"
                :key="`line-two-${word}-${index}`"
                class="reveal-mask"
                :style="{ '--delay': `${1960 + index * 180}ms` }"
              >
                <span class="reveal-segment title-word">{{ word }}</span>
              </span>
            </span>
          </h1>
        </div>

        <nav class="hero-nav" :class="{ 'is-revealed': animationStarted }" aria-label="Primary sections">
          <a v-for="link in navLinks" :key="link.href" :href="link.href" class="nav-link">
            {{ link.label }}
          </a>
        </nav>
      </div>
    </div>

    <div class="hero-figure-section">
      <div class="hero-figure-card">
        <img
          :src="asset('images/fig2.jpg')"
          alt="Paper Figure / System Overview"
          class="hero-fig-img"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref, watch } from 'vue'

const props = defineProps({
  animateOnReady: {
    type: Boolean,
    default: true,
  },
})

const asset = (relativePath) => `${import.meta.env.BASE_URL}${relativePath.replace(/^\/+/, '')}`

const navLinks = [
  { href: '#teaser', label: 'Interface' },
  { href: '#abstract', label: 'Abstract' },
  { href: '#video', label: 'Video' },
  { href: '#dataset', label: 'Dataset' },
  { href: '#code', label: 'Attention Quantification Framework' },
  { href: '#references', label: 'References' },
]

const titleLineOneWords = ['Student', 'Attention', 'Visualization']
const titleLineTwoWords = ['for', 'Video-based', 'Learning', 'Analysis']

const heroBackgroundStyle = {
  backgroundImage: `url(${asset('images/teaser.jpg')})`,
}

const animationStarted = ref(false)
const shadowVisible = ref(false)

let animationTimer = null
let shadowTimer = null

const startEntranceAnimation = () => {
  animationStarted.value = false
  shadowVisible.value = false

  if (animationTimer) {
    window.clearTimeout(animationTimer)
  }

  if (shadowTimer) {
    window.clearTimeout(shadowTimer)
  }

  animationTimer = window.setTimeout(() => {
    animationStarted.value = true
  }, 520)

  shadowTimer = window.setTimeout(() => {
    shadowVisible.value = true
  }, 3460)
}

onMounted(() => {
  if (props.animateOnReady) {
    startEntranceAnimation()
  }
  window.addEventListener('pageshow', startEntranceAnimation)
})

watch(
  () => props.animateOnReady,
  (ready, previousReady) => {
    if (ready && !previousReady) {
      startEntranceAnimation()
    }
  },
)

onBeforeUnmount(() => {
  if (animationTimer) {
    window.clearTimeout(animationTimer)
  }
  if (shadowTimer) {
    window.clearTimeout(shadowTimer)
  }
  window.removeEventListener('pageshow', startEntranceAnimation)
})
</script>

<style scoped>
.hero-wrap {
  width: 100%;
  background: #09131d;
}

.hero-screen {
  position: relative;
  min-height: 100svh;
  overflow: hidden;
  display: flex;
  align-items: stretch;
  justify-content: center;
}

.hero-bg,
.hero-overlay {
  position: absolute;
  inset: 0;
}

.hero-bg {
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  transform: scale(1.08);
  filter: blur(16px) saturate(0.95);
}

.hero-overlay {
  background:
    radial-gradient(circle at center, rgba(255, 255, 255, 0.08) 0%, rgba(255, 255, 255, 0.02) 26%, rgba(7, 16, 26, 0.40) 56%, rgba(7, 16, 26, 0.82) 100%),
    linear-gradient(180deg, rgba(7, 16, 26, 0.30) 0%, rgba(7, 16, 26, 0.58) 68%, rgba(7, 16, 26, 0.90) 100%);
}

.hero-content {
  position: relative;
  z-index: 1;
  width: min(1200px, calc(100% - 48px));
  min-height: 100svh;
  padding: clamp(36px, 5vw, 56px) 0 clamp(28px, 4vw, 44px);
  display: grid;
  grid-template-rows: 1fr auto;
  align-items: center;
}

.hero-center {
  width: min(980px, 100%);
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: clamp(14px, 2vw, 20px);
  text-align: center;
}

.logo-stack {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-bottom: 6px;
  opacity: 0;
  transform: translate3d(0, 22px, 0) scale(0.96);
}

.logo-stack.is-revealed {
  animation: visLogoReveal 1180ms cubic-bezier(0.22, 1, 0.36, 1) 180ms forwards;
}

.logo {
  display: block;
  max-width: 100%;
  object-fit: contain;
  filter: drop-shadow(0 10px 28px rgba(0, 0, 0, 0.28));
}

.logo-vis {
  width: min(360px, 62vw);
}

.paper-title {
  margin: 0;
  color: #ffffff;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: clamp(2rem, 3.8vw, 4rem);
  font-weight: 600;
  line-height: 1.04;
  letter-spacing: -0.03em;
  text-wrap: balance;
  text-shadow: none;
  transition: text-shadow 420ms ease, filter 420ms ease;
}

.paper-title.is-shadow-visible {
  text-shadow: 0 3px 8px rgba(0, 0, 0, 0.62), 0 1px 2px rgba(0, 0, 0, 0.5), 0 0 2px rgba(0, 0, 0, 0.45), 0 16px 36px rgba(0, 0, 0, 0.5), 0 8px 20px rgba(0, 0, 0, 0.38);
}

.paper-title.is-shadow-visible .reveal-mask {
  overflow: visible;
}

.title-line {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: clamp(8px, 0.9vw, 14px);
  white-space: nowrap;
}

.title-line + .title-line {
  margin-top: 0.08em;
}

.title-line-with-logo {
  flex-wrap: nowrap;
}

.title-line-two {
  gap: clamp(10px, 1vw, 15px);
}

.reveal-mask {
  display: inline-flex;
  overflow: hidden;
  padding-block: 0.08em 0.14em;
}

.reveal-segment {
  display: inline-flex;
  align-items: center;
  opacity: 0;
  transform: translate3d(0, 115%, 0) scale(0.92);
  filter: blur(10px);
  will-change: transform, opacity, filter;
}

.paper-title.is-revealed .reveal-segment {
  animation: textyReveal 980ms cubic-bezier(0.22, 1, 0.36, 1) forwards;
  animation-delay: var(--delay, 0ms);
}

  .inline-logo-group {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    flex: 0 0 auto;
    transform: translateY(0.02em);
  }


  .inline-savvy-logo {
    width: clamp(208px, 13.6vw, 295px);
    max-width: 43vw;
    flex: 0 0 auto;
    object-fit: contain;
    filter: brightness(0) invert(1) drop-shadow(0 8px 24px rgba(0, 0, 0, 0.28));
    transform: translateY(2px) scaleY(1.12);
    transform-origin: center bottom;
    opacity: 0.98;
  }


.inline-logo-colon {
  display: inline-block;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 0.95em;
  font-weight: 600;
  line-height: 1;
}

.title-word {
  display: inline-block;
}

.hero-nav {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 12px;
  align-self: end;
  opacity: 0;
  transform: translateY(16px);
}

.hero-nav.is-revealed {
  animation: navReveal 720ms ease forwards;
  animation-delay: 2680ms;
}

.nav-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 44px;
  padding: 10px 18px;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.26);
  background: rgba(255, 255, 255, 0.10);
  color: #ffffff;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 0.96rem;
  font-weight: 500;
  text-decoration: none;
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.18);
  transition:
    transform 0.22s ease,
    background-color 0.22s ease,
    border-color 0.22s ease;
}

.nav-link:hover {
  transform: translateY(-2px);
  background: rgba(255, 255, 255, 0.18);
  border-color: rgba(255, 255, 255, 0.42);
}

.hero-figure-section {
  padding: clamp(32px, 5vw, 56px) clamp(16px, 4vw, 24px) clamp(44px, 6vw, 72px);
  background: linear-gradient(180deg, #09131d 0%, #0d1824 100%);
}

.hero-figure-card {
  width: min(1200px, 100%);
  margin: 0 auto;
  border-radius: 24px;
  overflow: hidden;
  background: rgba(255, 255, 255, 0.96);
  box-shadow: 0 18px 48px rgba(0, 0, 0, 0.22);
}

.hero-fig-img {
  display: block;
  width: 100%;
  height: auto;
  object-fit: contain;
}

@keyframes visLogoReveal {
  0% {
    opacity: 0;
    transform: translate3d(0, 22px, 0) scale(0.96);
    filter: blur(12px);
  }
  60% {
    opacity: 1;
    transform: translate3d(0, 0, 0) scale(1.012);
    filter: blur(0);
  }
  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0) scale(1);
    filter: blur(0);
  }
}

@keyframes textyReveal {
  0% {
    opacity: 0;
    transform: translate3d(0, 115%, 0) scale(0.92);
    filter: blur(10px);
  }
  58% {
    opacity: 1;
    transform: translate3d(0, -6%, 0) scale(1.01);
    filter: blur(0);
  }
  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0) scale(1);
    filter: blur(0);
  }
}

@keyframes navReveal {
  from {
    opacity: 0;
    transform: translateY(16px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (prefers-reduced-motion: reduce) {
  .logo-stack,
  .hero-nav,
  .reveal-segment {
    opacity: 1 !important;
    transform: none !important;
    filter: none !important;
    animation: none !important;
  }
}

@media (max-width: 900px) {
  .hero-content {
    width: min(100%, calc(100% - 32px));
  }

  .paper-title {
    line-height: 1.18;
  }
}

@media (max-width: 640px) {
  .hero-content {
    padding-top: max(32px, env(safe-area-inset-top));
    padding-bottom: max(24px, env(safe-area-inset-bottom));
  }

  .logo-stack {
    gap: 10px;
    margin-bottom: 4px;
  }

  .logo-vis {
    width: min(280px, 72vw);
  }

  .paper-title {
    font-size: clamp(1.72rem, 8vw, 2.7rem);
    line-height: 1.12;
  }

  .title-line {
    flex-wrap: wrap;
    white-space: normal;
  }

  .title-line-with-logo {
    gap: 8px;
  }

  .inline-logo-group {
    gap: 3px;
  }

  .inline-savvy-logo {
    width: min(170px, 45vw);
    max-width: 100%;
  }

  .hero-nav {
    gap: 10px;
  }

  .nav-link {
    width: 100%;
  }

  .hero-figure-card {
    border-radius: 18px;
  }
}
</style>
