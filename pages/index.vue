<template>
  <v-container fluid>
    <div class="intro mt-5 mb-8">
      <h1 class="text-h1">
        Strategic Design
      </h1>

      <h2 class="mt-2">
        100x Your Nuxt.js skills
      </h2>
    </div>
    <v-row class="posts-container">
      <v-col cols="12">
        <div class="filter">
          <v-select
            v-model="category"
            style="width: 100px"
            outlined
            dense
            hide-details="auto"
            :items="['all', 'coding', 'youtube']"
          />
        </div>
      </v-col>

      <v-col v-for='post in posts' :key="post.slug" cols="12" md="6">
        <v-card elevation="0">
          <v-card-title> My first blog </v-card-title>
          <v-card-text>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad at corporis dolores excepturi, facilis impedit iure, molestiae molestias officia quae, quas similique soluta temporibus? Autem blanditiis consectetur neque optio veniam.
          </v-card-text>
          <v-card-actions>
            <v-btn text to="/1">Read more</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>

    <v-row class="post-pagination">
      <v-col class="text-right" cols="12">
        <v-btn>
          <v-icon small> mdi-arrow-left </v-icon>
          Previous
        </v-btn>
        <v-btn>
          Next
          <v-icon small> mdi-arrow-right </v-icon>
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Homepage',
  layout: 'DefaultLayout',
  async asyncData({ $content }) {
    const limit = 5
    const page = 1

    const fetchedPosts = await $content()
      .limit(limit)
      .sortBy('createdAt', 'desc')
      .skip((limit - 1) * (page - 1))
      .fetch()

    const nextPage = fetchedPosts.length === limit
    const posts = nextPage ? fetchedPosts.slice(0, -1) : fetchedPosts

    return {
      page,
      limit,
      posts,
      nextPage,
    }
  },

  data: () => ({
    category: 'all'
  }),

  mounted() {
    console.log(this.posts);
  }
}
</script>

<style>

</style>
