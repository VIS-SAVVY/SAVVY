<template>
  <section id="dataset" class="section-dark sec-pad">
    <div class="inner">
      <h2 class="sec-title">Dataset</h2>
      <div class="divider"></div>

      <!-- Description -->
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
          <strong>Partial Release.</strong> The dataset currently available for download is a
          representative subset of the full collection. The complete dataset will be publicly
          released upon acceptance of the paper.
        </p>
      </div>

      <!-- Download button -->
      <div class="dl-wrap">
        <a
          class="dl-btn"
          href="https://d2xsxph8kpxj0f.cloudfront.net/310519663469704594/Zt6AJnE8mLkXJTaJ9vvXXE/dataset_4077e4ac.zip"
          download="SAVVY_dataset_partial.zip"
          target="_blank"
          rel="noopener noreferrer"
        >
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="dl-icon">
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
            <polyline points="7 10 12 15 17 10"/>
            <line x1="12" y1="15" x2="12" y2="3"/>
          </svg>
          Download Partial Dataset (ZIP, ~129 MB)
        </a>
      </div>
    </div>
  </section>
</template>



<style scoped>
.sec-title {
  font-family: Arial, sans-serif;
  font-size: 28.8px;
  font-weight: 700;
  color: var(--text);
  text-align: center;
  margin-bottom: 12px;
}

.ds-desc {
  font-family: Arial, sans-serif;
  font-size: 16px;
  color: var(--muted);
  line-height: 1.85;
  max-width: 820px;
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
  max-width: 820px;
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

.notice-box strong {
  color: #4ade80;
}

/* Download button */
.dl-wrap {
  display: flex;
  justify-content: center;
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
  transition: background 0.2s, transform 0.15s;
}

.dl-btn:hover {
  background: #22c55e;
  transform: translateY(-2px);
}

.dl-icon {
  width: 18px;
  height: 18px;
  flex-shrink: 0;
}
</style>
