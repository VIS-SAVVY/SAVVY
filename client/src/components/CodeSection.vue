<template>
  <section id="code" class="section-dark">
    <div class="inner">
      <h2 class="sec-title">Attention Quantification Framework</h2>
      <div class="sec-divider"></div>

      <!-- Step 1: Fusion -->
      <div class="step-card">
        <div class="step-header">
          <span class="step-num">01</span>
          <div>
            <h3 class="step-title">Multimodal Signal Fusion</h3>
            <p class="step-desc">
              EEG-derived priors are used to fit a GLM (<em>Y = G&beta; + &epsilon;</em>) on fNIRS
              HbO/HbR signals. CSP features and Welch/DWT spectral features are then concatenated
              into a unified fused feature set
              <em>z<sup>(i)</sup> = [f<sup>(i)</sup><sub>EEG</sub>; f<sup>(i)</sup><sub>fNIRS</sub>]</em>.
            </p>
          </div>
        </div>
        <div class="code-label">Fusion — EEG-Informed GLM (Y = Gβ + ε)</div>
        <pre class="code-block"><code>for window_idx in range(n_windows):
    start = window_idx * step_size
    Y = fnirs_signal[start:start + window_size].reshape(-1, 1)
    G = design_matrix[start:start + window_size, :]
    beta = np.linalg.lstsq(G, Y, rcond=None)[0].flatten()
    beta_sequence.append(beta)

fused = np.concatenate([eeg_csp_features, hbo_features, hbr_features], axis=1)</code></pre>
      </div>

      <!-- Step 2: DDQN -->
      <div class="step-card">
        <div class="step-header">
          <span class="step-num">02</span>
          <div>
            <h3 class="step-title">DDQN-Based Attention Classification</h3>
            <p class="step-desc">
              A DDQN agent maps fused features <em>s<sub>t</sub></em> to attention levels via
              <em>Q(s<sub>t</sub>, a)</em>. Rewards are confidence-weighted:
              <em>r<sub>t</sub> = (&alpha; I(&ycirc;<sub>t</sub>=y<sub>t</sub>) &minus; &beta;(1&minus;I(&ycirc;<sub>t</sub>=y<sub>t</sub>))) c<sub>t</sub></em>
              (&alpha;=10, &beta;=&minus;1). The loss is
              <em>L<sub>DDQN</sub> = L<sub>TD</sub> + &lambda;L<sub>epi</sub></em>.
            </p>
          </div>
        </div>
        <div class="code-label">DDQN — Confidence-Based Reward + Hybrid Exploration</div>
        <pre class="code-block"><code>probs = torch.softmax(q_values, dim=1)
confidence = probs.max(dim=1)[0]
correct = (predictions == y_true).float()
rewards = (10.0 * correct - 1.0 * (1.0 - correct)) * confidence

p_soft = np.exp(q / temperature) / np.exp(q / temperature).sum(axis=1, keepdims=True)
p_hybrid = (1 - self.epsilon) * p_soft + self.epsilon / self.output_size

next_actions = self.q_network(next_states).argmax(dim=1)
target_q = self.target_network(next_states).gather(1, next_actions.unsqueeze(1)).squeeze(1)
td_loss = F.mse_loss(q_selected, rewards + gamma * target_q * (1 - dones))
loss = td_loss + 0.1 * episode_loss</code></pre>
      </div>

      <!-- Step 3: Audiovisual Density -->
      <div class="step-card">
        <div class="step-header">
          <span class="step-num">03</span>
          <div>
            <h3 class="step-title">Audiovisual Information Density Estimation</h3>
            <p class="step-desc">
              mTRF encoding and two-set variance partitioning decompose attention into visual,
              auditory, and shared contributions. Visual density combines edge density and IDF
              surprisal: <em>D<sub>vis</sub> = (w<sub>img</sub>c<sub>ED</sub> + w<sub>txt</sub>b&#x0305;<sub>S</sub>) / &Delta;t</em>;
              auditory density uses Shannon word-distribution entropy normalized by <em>&Delta;t</em>.
              For full implementation details, please refer to:
            </p>
            <ul class="ref-list">
              <li>
                <span class="ref-tag">[3]</span>
                R. Rosenholtz, Y. Li, and L. Nakano. Measuring visual clutter.
                <em>Journal of Vision</em>, 7(2):17, 2007.
              </li>
              <li>
                <span class="ref-tag">[4]</span>
                S. Ceri, A. Bozzon, M. Brambilla, E. Della Valle, P. Fraternali, and S. Quarteroni.
                An introduction to information retrieval. In <em>Web Information Retrieval</em>,
                pp. 3–11. Springer, 2013.
              </li>
              <li>
                <span class="ref-tag">[5]</span>
                C. E. Shannon. A mathematical theory of communication.
                <em>The Bell System Technical Journal</em>, 27(3):379–423, 1948.
              </li>
            </ul>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<script setup lang="ts">
// Attention Quantification Framework
// Design: Deep Space Academic — Arial body, Courier New code, blue-gradient bg
</script>

<style scoped>
.section-dark {
  width: 100%;
  padding: 5rem 0;
  background: linear-gradient(160deg, #13131f 0%, #16213e 50%, #0f3460 100%);
}

.inner {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 2rem;
}

.sec-title {
  font-family: Arial, sans-serif;
  font-size: 28.8px;
  font-weight: 700;
  color: #ffffff;
  text-align: center;
  margin: 0 0 0.75rem;
}

.sec-divider {
  width: 48px;
  height: 3px;
  background: #4ade80;
  margin: 0 auto 3rem;
  border-radius: 2px;
}

.step-card {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 2rem;
  margin-bottom: 2rem;
}

.step-header {
  display: flex;
  gap: 1.25rem;
  align-items: flex-start;
  margin-bottom: 1.25rem;
}

.step-num {
  font-family: Arial, sans-serif;
  font-size: 28px;
  font-weight: 700;
  color: #4ade80;
  opacity: 0.6;
  line-height: 1;
  flex-shrink: 0;
  min-width: 2.5rem;
}

.step-title {
  font-family: Arial, sans-serif;
  font-size: 22.4px;
  font-weight: 700;
  color: #e2e8f0;
  margin: 0 0 0.6rem;
}

.step-desc {
  font-family: Arial, sans-serif;
  font-size: 16px;
  color: #94a3b8;
  line-height: 1.7;
  margin: 0;
}

.code-label {
  font-family: Arial, sans-serif;
  font-size: 13px;
  font-weight: 600;
  color: #4ade80;
  margin-bottom: 0.5rem;
  letter-spacing: 0.02em;
}

.code-block {
  background: rgba(0, 0, 0, 0.45);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  padding: 1.25rem 1.5rem;
  overflow-x: auto;
  margin: 0;
}

.code-block code {
  font-family: 'Courier New', Courier, monospace;
  font-size: 14px;
  color: #e2e8f0;
  line-height: 1.65;
  white-space: pre;
}

.ref-list {
  list-style: none;
  padding: 0;
  margin: 1rem 0 0;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.ref-list li {
  font-family: Arial, sans-serif;
  font-size: 15px;
  color: #94a3b8;
  line-height: 1.6;
  display: flex;
  gap: 0.6rem;
  align-items: flex-start;
}

.ref-tag {
  font-family: Arial, sans-serif;
  font-size: 13px;
  font-weight: 700;
  color: #4ade80;
  background: rgba(74, 222, 128, 0.12);
  border-radius: 4px;
  padding: 1px 6px;
  flex-shrink: 0;
  margin-top: 2px;
}

@media (max-width: 600px) {
  .step-header { flex-direction: column; gap: 0.5rem; }
  .step-num { font-size: 22px; }
  .sec-title { font-size: 22px; }
  .step-title { font-size: 18px; }
  .code-block code { font-size: 12px; }
}
</style>
