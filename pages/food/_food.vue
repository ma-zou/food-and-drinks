<template>
  <main>
    <nuxt-link class="branding" to="/"><span>Zoudlik's</span> Food</nuxt-link>
     <section v-if="post">
      <article>
        <div class="content">
          <h1 class="">{{ post.title }} <small>{{ amount }}</small></h1>
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
          <nuxt-link class="back" to="/food">Zurück zu Food</nuxt-link>
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
      post = await $content("food", params.food).fetch();
    } catch (e) {
      error({ message: "Blog post not found" });
    }
    return { post };
  },
  computed: {
    categories: function() {
      return this.post.category.join(' ꞏ ');
    },
    amount: function() {
      return this.post.amount > 1 ? this.post.amount + ' Personen' : '1 Person';
    }
  }
}
</script>
