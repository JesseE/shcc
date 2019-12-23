<template>
  <main class="main">
    <pageHeader />
    <section class="main__content">
      <pageTitle />
      <pageArticle />
      <lazyLoad>
        <animatedRect />
      </lazyLoad>
      <videoBlock />
    </section>
  </main>
</template>

<script>
export default {
  components: {
    lazyLoad: () => import('../components/lazy-load/lazy-load'),
    pageTitle: () => import('../components/page-title/page-title'),
    pageHeader: () => import('../components/page-header/page-header'),
    pageArticle: () => import('../components/page-article/page-article'),
    animatedRect: () => import('../components/animated-rect/animated-rect'),
    videoBlock: () => import('../components/video-block/video-block')
  },
};
</script>
