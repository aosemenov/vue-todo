<template>
  <component :is="currentPageComponent" :page-params="currentPageParams"></component>
</template>

<script>
import MainPage from './pages/MainPage.vue';
import ProductPage from './pages/ProductPage.vue';
import NotFoundPage from './pages/NotFoundPage.vue';
import eventBus from './eventBus';

const routes = {
  main: 'MainPage',
  product: 'ProductPage',
};

export default {
  data() {
    return {
      currentPage: 'main',
      currentPageParams: {},
    };
  },
  components: {
    MainPage, ProductPage, NotFoundPage,
  },
  methods: {
    gotoPage(pageName, pageParams) {
      this.currentPage = pageName;
      this.currentPageParams = pageParams || {};
    },
  },
  computed: {
    currentPageComponent() {
      return routes[this.currentPage] || 'NotFoundPage';
    },
  },
  created() {
    eventBus.$on('gotoPage', (pageName, pageParams) => this.gotoPage(pageName, pageParams));
  },
};
</script>

<style>

</style>
