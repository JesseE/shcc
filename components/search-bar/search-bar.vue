<template>
  <form>
    <label for="search">
      <input class="search__input" type="text" id="search" placeholder="Search" />
      <searchIcon class="search__icon"/>
    </label>
  </form>
</template>

<script>
import searchIcon from '../../images/icons/search.svg'

export default {
  name:'searchBar',
  components: {
    searchIcon
  }
}
</script>
