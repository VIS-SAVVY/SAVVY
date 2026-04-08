<template>
  <section id="video" class="section-dark sec-pad">
    <div class="inner">
      <h2 class="sec-title">Video</h2>
      <div class="divider"></div>

      <!-- 主视频区域 -->
      <div class="video-wrap">
        <video
          class="main-video"
          controls
          preload="metadata"
          poster=""
        >
          <source src="https://dataset-1341757241.cos.ap-nanjing.myqcloud.com/SAVVY_Video.mp4" type="video/mp4" />
          Your browser does not support the video tag.
        </video>
      </div>

      <p class="video-caption">Main Demo Video</p>
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
.divider {
  width: 52px; height: 3px;
  background: var(--accent);
  border-radius: 2px;
  margin: 0 auto 2.5rem;
}
.video-wrap {
  width: 100%;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 32px rgba(0,0,0,.4);
  border: 1px solid var(--border);
  background: #000;
}
.main-video {
  width: 100%;
  display: block;
  aspect-ratio: 16/9;
  object-fit: contain;
  background: #000;
}
.video-caption {
  text-align: center;
  margin-top: 1rem;
  font-family: Arial, sans-serif;
  font-size: 14px;
  color: var(--muted);
  opacity: 0.75;
}
</style>
