<template>
  <nav>
    <ul class="nav-list">
      <li class="nav-list__item"
        v-for="({ link, title }, index) in this.navigation" :key="index">
        <a :href="link" class="nav-list__item-link">{{title}}</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "navList",
  data() {
    return {
      navigation: [{
          link: "",
          title: "Women"
        },{
          link: "",
          title: "Men"
        },{
          link: "",
          title: "Kids"
        },{
          link: "",
          title: "Labels"
        },{
          link: "",
          title: "Sale"
        }]
    };
  }
};
</script>
