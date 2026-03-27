<template>
  <div id="app">
    <HeroSection />
    <TeaserSection />
    <AbstractSection />
    <VideoSection />
    <DatasetSection />
    <CodeSection />
    <ReferencesSection />
  </div>
</template>

<script setup>
import HeroSection       from './components/HeroSection.vue'
import TeaserSection     from './components/TeaserSection.vue'
import AbstractSection   from './components/AbstractSection.vue'
import VideoSection      from './components/VideoSection.vue'
import DatasetSection    from './components/DatasetSection.vue'
import CodeSection       from './components/CodeSection.vue'
import ReferencesSection from './components/ReferencesSection.vue'
</script>

<style>
#app {
  min-height: 100vh;
  width: 100%;
  max-width: none !important;
  overflow-x: hidden;
}
</style>
