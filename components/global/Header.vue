<template>
  <div>
      <nuxt-link class="branding" to="/"><span>Zoudlik's</span> {{ pageCat }}</nuxt-link>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      subPage: 'Recipies',
      subPageLink: ''
    }
  },
  computed: {
    pageCat: function() {
      return this.subPage = (this.$router.currentRoute.name === 'index') ? 'Recipies' : this.$router.currentRoute.fullPath.split('/')[1];
    }
  }
}
</script>