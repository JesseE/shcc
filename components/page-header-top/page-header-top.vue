<template>
  <div class="page-header-top">
    <div class="page-header-top__block">
      <span class="page-header-top__block-text">UK/GBP(&pound;)</span>
      <span class="page-header-top__block-text">STORES</span>
      <span class="page-header-top__block-text">CUSTOMER SERVICE</span>
    </div>
    <div class="page-header-top__block">
      <span class="page-header-top__block-text page-header-top__block-text--italic">
        Enjoy free delivery on all orders over &pound;50
      </span>
    </div>
    <div class="page-header-top__block">
      <span class="page-header-top__block-text">newsletter sign up</span>
      <span class="page-header-top__block-text">sign in / register</span>
      <shoppingBagIcon class="page-header-top__block-image"/>
    </div>
  </div>
</template>

<script>
import shoppingBagIcon from '../../images/icons/shopping-bag.svg';

export default {
  name: 'pageHeaderTop',
  components: {
    shoppingBagIcon
  }
}
</script>
