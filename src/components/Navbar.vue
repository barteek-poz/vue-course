<template>
  <nav
    class="navbar navbar-expand-lg"
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
    <div class="container-fluid">
      <a href="#" class="navbar-brand">My Vue</a>
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <navbar-link
          v-for="(page, index) in filteredPages"
          :page="page"
          :index="index"
          :key="index"></navbar-link>
        <li>
          <router-link :to="`/pages`" aria-current="page" class="nav-link" active-class="active"
            >Pages</router-link
          >
        </li>
      </ul>
    </div>
    <form class="d-flex">
      <button @click.prevent="changeTheme" class="btn btn-primary">
        Change theme
      </button>
    </form>
  </nav>
</template>

<script>
import NavbarLink from "./NavbarLink.vue";
export default {
  components: {
    NavbarLink,
  },
  inject: ['$pages', '$bus'],
  created() {
    this.getThemeSetting();
    this.pages = this.$pages.getAllPages()
    this.$bus.$on('page-update', ()=> {
      this.pages = [...this.$pages.getAllPages()]
    })
    this.$bus.$on('page-created', ()=> {
      this.pages = [...this.$pages.getAllPages()]
    })
    this.$bus.$on('page-removed', ()=> {
      this.pages = [...this.$pages.getAllPages()]
    })
  },
  computed: {
    filteredPages() {
      return this.pages.filter((page) => page.published);
    },
  },
  data() {
    return {
      theme: "dark",
      pages: []
    };
  },
  methods: {
    changeTheme() {
      let theme = "light";
      if (this.theme === "light") {
        theme = "dark";
      }
      this.theme = theme;
      this.storeThemeSetting();
    },
    storeThemeSetting() {
      localStorage.setItem("theme", this.theme);
    },
    getThemeSetting() {
      const theme = localStorage.getItem("theme");
      if (theme) {
        this.theme = theme;
      }
    },
  },
};
</script>
