<template>
  <main>
    <nuxt-link class="branding" to="/"><span>Zoudlik's</span> Drinks</nuxt-link>
    <section v-if="post">
      <article>
        <div class="content">
          <h1 class="">{{ post.title }}</h1>
          <div class="col-1">
            <div v-if="post.cover" class="image">
              <img
                class="cover-image"
                :src="post.cover"
              >
            </div>
            <h6>{{ categories }}</h6>
          </div>
          <div class="col-2">
            <p class="desc">{{ post.description }}</p>
          </div>
          <nuxt-content class="ingredients" :document="post" />
          <p class="info">{{ post.info }}</p>
          <nuxt-link class="back" to="/drinks">Zurück zu Drinks</nuxt-link>
        </div>
      </article>
    </section>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    let post;
    try {
      // console.log($content("drinks").fetch());
      post = await $content("drinks", params.drinks).fetch();
    } catch (e) {
      error({ message: "Project not found" });
    }
    return { post };
  },
  computed: {
    categories: function() {
      return this.post.category.join(' ꞏ ');
    }
  }
}
</script>
