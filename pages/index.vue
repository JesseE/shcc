<template>
  <main class="main">
    <pageHeader />
    <section class="main__content">
      <pageTitle />
      <pageArticle />
      <video class="video-block">
        <source src="../assets/test-video.mp4" type="video/mp4" />
        <div></div>
      </video>
    </section>
  </main>
</template>

<script>
  export default {
    components: {
      pageTitle: () => import('../components/page-title/page-title'),
      pageHeader: () => import('../components/page-header/page-header'),
      pageArticle: () => import('../components/page-article/page-article')
    },
  };
</script>

<style>
  .video-block {
    margin-left: 90px;
    position: relative;
    top:-80px;
    width: 800px;
    height: 520px;
  }
</style>
