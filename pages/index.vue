<template>
  <section id="posts">
    <PostPreview
    v-for="post in posts"
    :key="post.id"
    :title="post.title"
    :excerpt="post.previewText"
    :thumbnailImage="post.thumbnailUrl"
    :id="post.id" />
  </section>
</template>

<script>
import PostPreview from "@/components/Blog/PostPreview";
export default {
  components: {
    PostPreview
  },
  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories', {
      version: 'draft',
      starts_with: 'blog/'
    }).then(res => {
      return {
        posts: res.data.stories.map(bp => {
        return {
          id: bp.slug,
          title: bp.content.title,
          previewText: bp.content.summary,
           thumbnailUrl: bp.content.thumbnail
        }
      })
    };
    });
  }
  // data() {
  //   return {
  //     posts: [
  //       {
  //         title: 'Vue The Future First Post',
  //         previewText: 'The Beggining to your future Vue',
  //         thumbnailUrl: 'https://www.studenty.cn/wp-content/uploads/2018/01/2018011314024962.png',
  //         id: 'vue-the-future-first'
  //     },
  //     {
  //       title: 'Vue The Future Second Post',
  //       previewText: 'The First Step to your future Vue',
  //       thumbnailUrl:'https://d2eip9sf3oo6c2.cloudfront.net/series/square_covers/000/000/083/landscape/EGH_VueJS_Final.png',
  //       id: 'vue-the-future-second'
  //   }
  //   ]
  //   }
  // }
}
</script>

<style>
    #posts {
      padding-top: 2rem;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
    }
    @media(min-width: 35rem) {
        #posts {
          flex-direction: row;
        }
    }
</style>
