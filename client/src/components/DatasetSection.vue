<template>
  <section id="dataset" class="section-dark sec-pad">
    <div class="inner">
      <h2 class="sec-title">Dataset</h2>
      <div class="divider"></div>

      <!-- ① Dataset Form Preview -->
      <h3 class="sub-title">Dataset Form Preview</h3>
    </div>
    <!-- Full-width image breakout -->  
    <div class="processing-full-wrap">
      <div class="processing-img-box">
        <img
          src="/images/dataset_table1.jpg"
          alt="Dataset sample: EEG & Motion data (Sxx)"
          class="processing-img"
        />
      </div>
      <div class="processing-img-box" style="margin-top:1rem;">
        <img
          src="/images/dataset_table2.jpg"
          alt="Dataset sample: fNIRS data (Sxx)"
          class="processing-img"
        />
      </div>
      <div class="inner">
      <p class="processing-note">
        <strong>Note:</strong> The tables above are a <em>sample illustration</em> of the dataset format,
        split by signal type (EEG &amp; Motion / fNIRS).
        The column structure and data types faithfully reflect the actual recordings, but all numerical
        values shown are <strong>simulated and do not represent real experimental measurements</strong>.
        The complete dataset with authentic data will be made publicly available upon acceptance of the paper.
      </p>
      </div>
    </div>
    <div class="inner">

      <!-- ② Dataset Description -->
      <h3 class="sub-title">Dataset Description</h3>
      <p class="ds-desc">
        We collected a multimodal brain dataset from 31 healthy participants (16 male, 15 female;
        mean age 23.6 ± 1.2 years) while they watched instructional videos on three topics:
        Convolutional Neural Networks, Matrix Factorization, and Neurons and Synapses. Each session
        lasted approximately 30 ± 5.8 minutes. Signals were recorded using the LoongX
        Neurophysiological Headband, which simultaneously captures 2 EEG channels (Fp1, Fp2) at
        128 Hz and 8 fNIRS channels (S1D1–S1D4, S2D5–S2D8) at 25 Hz, covering the prefrontal
        cortex. External attention-modulating stimuli were introduced during the experiment to
        establish ground-truth labels of three attention levels: high, medium, and low. The dataset
        contains over 4.5 million data points in total.
      </p>

      <!-- Partial release notice -->
      <div class="notice-box">
        <svg class="notice-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="12" cy="12" r="10"/>
          <line x1="12" y1="8" x2="12" y2="12"/>
          <line x1="12" y1="16" x2="12.01" y2="16"/>
        </svg>
        <p>
          <strong>Dataset Availability.</strong> The dataset is not currently available for download.
          Download links will be provided upon acceptance of the paper.
          The download buttons below are disabled at this time.
        </p>
      </div>

      <!-- ④ Full ZIP download (disabled) -->
      <div class="dl-wrap">
        <span class="dl-btn dl-btn-disabled">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="dl-icon">
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
            <polyline points="7 10 12 15 17 10"/>
            <line x1="12" y1="15" x2="12" y2="3"/>
          </svg>
          Download Partial Dataset (ZIP, ~129 MB)
        </span>
      </div>

      <!-- ④ Per-participant download cards -->
      <div class="per-part-section">
        <h3 class="sub-title" style="margin-top:2.8rem;">Individual Participant Data</h3>
        <p class="ds-desc" style="margin-bottom:1.8rem;">
          Download data for each participant individually. Each file contains synchronized EEG and fNIRS recordings for one session (~35–57 MB per file).
        </p>

        <div class="part-grid">
          <span
            v-for="p in currentPageParticipants"
            :key="p.id"
            class="part-card part-card-disabled"
          >
            <div class="part-card-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
                <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
                <polyline points="14 2 14 8 20 8"/>
                <line x1="12" y1="18" x2="12" y2="12"/>
                <polyline points="9 15 12 18 15 15"/>
              </svg>
            </div>
            <div class="part-card-label">{{ p.name }}</div>
            <div class="part-card-sub">{{ p.size }}</div>
          </span>
        </div>

        <!-- Pagination -->
        <div class="pagination" v-if="totalPages > 1">
          <button
            class="page-btn"
            :disabled="currentPage === 1"
            @click="currentPage--"
          >
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" width="14" height="14">
              <polyline points="15 18 9 12 15 6"/>
            </svg>
          </button>
          <button
            v-for="p in totalPages"
            :key="p"
            class="page-btn"
            :class="{ active: p === currentPage }"
            @click="currentPage = p"
          >{{ p }}</button>
          <button
            class="page-btn"
            :disabled="currentPage === totalPages"
            @click="currentPage++"
          >
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" width="14" height="14">
              <polyline points="9 18 15 12 9 6"/>
            </svg>
          </button>
        </div>
      </div>

    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const PER_PAGE = 5

const participants = [
  { id: 1,  name: 'Subject 01',  filename: 'S1.csv',  size: '~35.6 MB', url: '' },
  { id: 2,  name: 'Subject 02',  filename: 'S2.csv',  size: '~35.2 MB', url: '' },
  { id: 3,  name: 'Subject 03',  filename: 'S3.csv',  size: '~33.9 MB', url: '' },
  { id: 4,  name: 'Subject 04',  filename: 'S4.csv',  size: '~35.6 MB', url: '' },
  { id: 5,  name: 'Subject 05',  filename: 'S5.csv',  size: '~38.5 MB', url: '' },
  { id: 6,  name: 'Subject 06',  filename: 'S6.csv',  size: '~35.6 MB', url: '' },
  { id: 7,  name: 'Subject 07',  filename: 'S7.csv',  size: '~35.1 MB', url: '' },
  { id: 8,  name: 'Subject 08',  filename: 'S8.csv',  size: '~34.3 MB', url: '' },
  { id: 9,  name: 'Subject 09',  filename: 'S9.csv',  size: '~35.0 MB', url: '' },
  { id: 10, name: 'Subject 10',  filename: 'S10.csv', size: '~54.4 MB', url: '' },
  { id: 11, name: 'Subject 11',  filename: 'S11.csv', size: '~38.2 MB', url: '' },
  { id: 12, name: 'Subject 12',  filename: 'S12.csv', size: '~38.9 MB', url: '' },
  { id: 13, name: 'Subject 13',  filename: 'S13.csv', size: '~51.0 MB', url: '' },
  { id: 14, name: 'Subject 14',  filename: 'S14.csv', size: '~34.9 MB', url: '' },
  { id: 15, name: 'Subject 15',  filename: 'S15.csv', size: '~34.8 MB', url: '' },
]

const currentPage = ref(1)
const totalPages = computed(() => Math.ceil(participants.length / PER_PAGE))
const currentPageParticipants = computed(() => {
  const start = (currentPage.value - 1) * PER_PAGE
  return participants.slice(start, start + PER_PAGE)
})
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

.sub-title {
  font-family: Arial, sans-serif;
  font-size: 18px;
  font-weight: 700;
  color: var(--text);
  max-width: 100%;
  margin: 0 auto 1.2rem;
  letter-spacing: 0.01em;
}

/* Processing image – full-width breakout */
.processing-full-wrap {
  width: 100%;
  padding: 0 clamp(16px, 3vw, 48px);
  box-sizing: border-box;
  margin-bottom: 0;
}

.processing-img-box {
  width: 100%;
  max-width: 1600px;
  margin: 0 auto 1.2rem;
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid var(--border);
  background: #ffffff;
  box-shadow: 0 4px 24px rgba(0,0,0,.3);
}

.processing-img {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 12px;
  object-fit: unset;
}

.processing-note {
  font-family: Arial, sans-serif;
  font-size: 14px;
  color: var(--muted);
  line-height: 1.75;
  margin: 0 auto 2.5rem;
  padding: 0.85rem 1.2rem;
  background: rgba(255, 255, 255, 0.04);
  border-left: 3px solid rgba(74, 222, 128, 0.55);
  border-radius: 0 8px 8px 0;
}

.processing-note strong { color: #e2e8f0; }
.processing-note em { color: #fbbf24; font-style: normal; font-weight: 600; }

.ds-desc {
  font-family: Arial, sans-serif;
  font-size: 16px;
  color: var(--muted);
  line-height: 1.85;
  max-width: 100%;
  margin: 0 auto 2.5rem;
  text-align: left;
}

/* Notice box */
.notice-box {
  display: flex;
  align-items: flex-start;
  gap: 0.9rem;
  background: rgba(74, 222, 128, 0.08);
  border: 1px solid rgba(74, 222, 128, 0.3);
  border-radius: 10px;
  padding: 1rem 1.4rem;
  max-width: 100%;
  margin: 0 auto 2.5rem;
}

.notice-icon {
  width: 20px;
  height: 20px;
  flex-shrink: 0;
  color: #4ade80;
  margin-top: 2px;
}

.notice-box p {
  font-family: Arial, sans-serif;
  font-size: 15px;
  color: var(--muted);
  line-height: 1.7;
  margin: 0;
}

.notice-box strong { color: #4ade80; }

/* Full ZIP download button */
.dl-wrap {
  display: flex;
  justify-content: center;
  margin-bottom: 0;
}

.dl-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  background: #4ade80;
  color: #0f1a2e;
  font-family: Arial, sans-serif;
  font-size: 15px;
  font-weight: 700;
  padding: 0.75rem 2rem;
  border-radius: 8px;
  text-decoration: none;
}

.dl-btn-disabled {
  background: rgba(255,255,255,0.12) !important;
  color: rgba(255,255,255,0.3) !important;
  cursor: not-allowed !important;
  pointer-events: none;
}

.dl-icon {
  width: 18px;
  height: 18px;
  flex-shrink: 0;
}

/* Per-participant section */
.per-part-section {
  max-width: 100%;
  margin: 0 auto;
}

/* Participant cards grid — 5 per row, fills the full width */
.part-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1rem;
  margin-bottom: 1.5rem;
}

/* Large card style matching original design */
.part-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  background: rgba(255,255,255,0.06);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 1.6rem 1rem;
  text-decoration: none;
  color: var(--text);
  min-height: 120px;
}

.part-card-disabled {
  opacity: 0.35;
  cursor: not-allowed !important;
  pointer-events: none;
}

.part-card-icon {
  width: 36px;
  height: 36px;
  color: var(--muted);
}

.part-card-icon svg {
  width: 100%;
  height: 100%;
}

.part-card-label {
  font-family: Arial, sans-serif;
  font-size: 14px;
  font-weight: 700;
  color: var(--text);
  letter-spacing: 0.02em;
}

.part-card-sub {
  font-family: Arial, sans-serif;
  font-size: 12px;
  color: var(--muted);
  opacity: 0.8;
}

/* Pagination */
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  margin-top: 0.5rem;
}

.page-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 38px;
  height: 38px;
  padding: 0 0.6rem;
  background: rgba(255,255,255,0.06);
  border: 1px solid var(--border);
  border-radius: 8px;
  color: var(--muted);
  font-family: Arial, sans-serif;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.18s, border-color 0.18s, color 0.18s;
}

.page-btn:hover:not(:disabled):not(.active) {
  background: rgba(74, 222, 128, 0.1);
  border-color: rgba(74, 222, 128, 0.4);
  color: #4ade80;
}

.page-btn.active {
  background: #4ade80;
  border-color: #4ade80;
  color: #0f1a2e;
}

.page-btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

@media (max-width: 600px) {
  .part-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
