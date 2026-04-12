<template>
  <div class="intro-overlay" aria-hidden="true">
    <div ref="animationContainer" class="intro-overlay__animation"></div>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const emit = defineEmits(['complete'])

const animationContainer = ref(null)
const LOADER_DURATION_MS = 2500
const BASE_URL = import.meta.env.BASE_URL || '/'
const withBase = (relativePath) => new URL(relativePath, window.location.origin + BASE_URL).toString()
const LOTTIE_SCRIPT_SRC = withBase('reference-loader/lottie.min.js')
const LOTTIE_DATA_PATH = withBase('reference-loader/data.json')

let completeTimer = null
let lottieAnimation = null
let lottieLoaderPromise = null

const loadLottie = () => {
  if (typeof window === 'undefined') {
    return Promise.resolve(null)
  }

  if (window.lottie) {
    return Promise.resolve(window.lottie)
  }

  if (lottieLoaderPromise) {
    return lottieLoaderPromise
  }

  lottieLoaderPromise = new Promise((resolve, reject) => {
    const existingScript = document.querySelector('script[data-loader="savvy-ref-lottie"]')

    if (existingScript) {
      existingScript.addEventListener('load', () => resolve(window.lottie), { once: true })
      existingScript.addEventListener('error', () => reject(new Error('Failed to load Lottie script.')), {
        once: true,
      })
      return
    }

    const script = document.createElement('script')
    script.src = LOTTIE_SCRIPT_SRC
    script.async = true
    script.dataset.loader = 'savvy-ref-lottie'
    script.onload = () => resolve(window.lottie)
    script.onerror = () => reject(new Error('Failed to load Lottie script.'))
    document.head.appendChild(script)
  })

  return lottieLoaderPromise
}

onMounted(async () => {
  try {
    const lottie = await loadLottie()

    if (lottie && animationContainer.value) {
      lottieAnimation = lottie.loadAnimation({
        container: animationContainer.value,
        renderer: 'svg',
        loop: false,
        autoplay: true,
        path: LOTTIE_DATA_PATH,
      })
    }
  } catch (error) {
    console.error('Unable to initialize reference intro animation.', error)
  }

  completeTimer = window.setTimeout(() => {
    emit('complete')
  }, LOADER_DURATION_MS)
})

onBeforeUnmount(() => {
  if (completeTimer !== null) {
    window.clearTimeout(completeTimer)
  }

  if (lottieAnimation) {
    lottieAnimation.destroy()
    lottieAnimation = null
  }
})
</script>

<style scoped>
.intro-overlay {
  position: fixed;
  inset: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background: #14141c;
  overflow: hidden;
}

.intro-overlay__animation {
  width: min(100vw, 1280px);
  height: min(100vh, 720px);
  max-width: 100%;
  max-height: 100%;
}

:global(.intro-fade-leave-active) {
  transition: opacity 0.4s ease;
}

:global(.intro-fade-leave-from) {
  opacity: 1;
}

:global(.intro-fade-leave-to) {
  opacity: 0;
}

@media (prefers-reduced-motion: reduce) {
  :global(.intro-fade-leave-active) {
    transition-duration: 0.01ms;
  }
}
</style>
