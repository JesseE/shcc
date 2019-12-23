<template>
  <header class="page-header">
    <div class="page-header__border-bottom">
      <pageHeaderTop />
    </div>
    <div class="page-header__container">
      <div class="page-header__container-image">
        <img src="../../images/logo.png" alt="tommy hilfiger logo"/>
      </div>
      <navList />
      <searchBar />
    </div>
  </header>
</template>

<script>
export default {
  name: "pageHeader",
  components: {
    searchBar: () => import('../search-bar/search-bar.vue'),
    pageHeaderTop: () => import('../page-header-top/page-header-top.vue'),
	  navList: () => import('../nav-list/nav-list.vue')
  }
};
</script>
