<template>
  <section id="abstract" class="section-dark sec-pad">
    <div class="inner">
      <h2 class="sec-title">Abstract</h2>
      <div class="divider"></div>
      <p class="abstract-body">
        Video-Based Learning (VBL) has become the primary delivery medium of education in the past decade, ranging from online
        education to hybrid learning. Students' rising expectations for video quality have motivated teachers to optimize instructional videos
        before releasing them. Analyzing student attention to guide course improvement offers an objective optimization strategy. However,
        existing attention quantification algorithms are highly susceptible to noise in real-world environments, degrading estimation accuracy.
        Moreover, even when attention data are available, teachers must still invest substantial effort in empirical revision attempts, limiting
        practical feasibility. To address these challenges, we first propose a novel attention quantification framework based on multimodal brain
        signals that enables unprecedentedly stable tracking of student attention levels. We then develop SAVVY, an interactive visual analytics
        system that integrates visual and auditory attention to support top-down exploration of student attention variations. SAVVY comprises
        three coordinated visualization modules. These modules incorporate multi-level information, including course content structure,
        audiovisual information density, and attentional resource allocation, and provide multi-temporal-resolution attention trajectories of
        individual students, enabling teachers to comprehensively analyze the underlying causes of attention fluctuations and inform their
        subsequent instructional video improvement. We evaluate SAVVY through quantitative experiments, two case studies, and expert
        interviews. The results demonstrate the effectiveness and usability of SAVVY in intuitively identifying student attention variations and
        supporting instructional video optimization.
      </p>
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
.abstract-body {
  font-size: 16px;
  color: var(--muted);
  line-height: 1.85;
  max-width: 720px;
  margin: 0 auto;
  text-align: left;
}
</style>
