<template>
  <li>
    <router-link
    :to="`/${index}`"
    :href="page.link.url"
    :title="`This link goes to ${page.link.text} page `"
    aria-current="page"
    class="nav-link"
    active-class="active "
    @click.prevent="$bus.$emit('navLinkActivated', index)"
    >{{ page.link.text }}</router-link>
  </li>

</template>

<script>
export default {
  props: ["page","index"],
};
</script>

