<template>
  <section id="abstract" class="section-dark sec-pad">
    <div class="abstract-inner">
      <h2 class="sec-title">Abstract</h2>
      <div class="divider"></div>
      <p class="abstract-body">
        Video-Based Learning (VBL) has become a popular delivery medium of education in the past decade, ranging from
        online education to hybrid learning. Students' rising expectations for video quality have motivated teachers to enhance the design of
        instructional videos before releasing them. Analyzing the attention of pilot cohorts in advance has become a conventional optimization
        strategy to guide course improvement. However, existing attention quantification algorithms are highly susceptible to noise in real-world
        environments, degrading estimation accuracy. Moreover, even when attention data are available, teachers must still invest substantial
        effort in empirical revision attempts, limiting practical feasibility. To address these challenges, we first propose a novel attention modeling
        framework based on multimodal brain signals that enables unprecedentedly stable tracking of student attention levels. We then develop
        SAVVY, a novel interactive visual analytics system that integrates visual and auditory attention to support top-down exploration of
        student attention variations. SAVVY comprises three coordinated visualization modules. These modules incorporate multi-level
        information, including course content structure, audiovisual information density, and attentional resource allocation, and provide
        multi-temporal-resolution attention trajectories of individual students, enabling teachers to comprehensively analyze the underlying
        causes of attention fluctuations and inform their subsequent instructional video improvement. We evaluate SAVVY through quantitative
        experiments, two case studies, and expert interviews. The results demonstrate the effectiveness and usability of SAVVY in intuitively
        identifying student attention variations and supporting instructional video optimization.
      </p>
    </div>
  </section>
</template>

<style scoped>
.abstract-inner {
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

.abstract-body {
  font-size: 16px;
  color: var(--muted);
  line-height: 1.85;
  max-width: 100%;
  margin: 0 auto;
  text-align: left;
}
</style>
