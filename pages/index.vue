<template>
  <main class="main">
    <pageHeader />
    <section class="main__content">
      <pageTitle />
      <pageArticle />
      <animatedRect />
      <videoBlock />
    </section>
  </main>
</template>

<script>
export default {
  components: {
    pageTitle: () => import('../components/page-title/page-title'),
    pageHeader: () => import('../components/page-header/page-header'),
    pageArticle: () => import('../components/page-article/page-article'),
    animatedRect: () => import('../components/animated-rect/animated-rect'),
    videoBlock: () => import('../components/video-block/video-block')
  },
};
</script>
