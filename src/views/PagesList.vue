<template>
  <h4>Pages</h4>
  <div class="text-end">
    <router-link to="/pages/create" class="btn btn-primary btn-small"
      >New page
    </router-link>
  </div>
  <table class="table table-hover">
    <thead>
      <tr>
        <th>Title</th>
        <th>Link text</th>
        <th>Is published</th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="(page, index) in $pages.getAllPages()"
        @click.prevent="goToPage(index)">
        <td>{{ page.pageTitle }}</td>
        <td>{{ page.linkText }}</td>
        <td>{{ page.published ? "Yes" : "No" }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import { inject } from "vue";
import { useRouter } from "vue-router";
const $pages = inject("$pages");
const router = useRouter();
function goToPage(index) {
  router.push({ path: `/pages/${index}/edit` });
}
</script>

<style scoped>
.table.table-hover tr:hover {
  cursor: pointer;
}
</style>
