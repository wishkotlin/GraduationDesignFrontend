<template>
  <block>
    <!-- <v-article
      :title="currentMovie.title"
      :user_name="currentMovie.user ? currentMovie.user.user_name : ''"
      :content="currentMovie.content || ''"
      :summary="currentMovie.summary || ''"
    ></v-article> -->
    <web-view :src="id"></web-view>
  </block>
</template>

<script>
import { mapState, mapActions } from 'vuex'
import article from '@/components/article'
export default {
  onLoad(query) {
    // this.clearMovieDetail()
    console.log(query);
    const id = query.id.replace(/[a-z\/:.]/gi, "") // 取av号
    this.id = `//player.bilibili.com/player.html?aid=${id}`
    
    console.log(this.id);
  },
  data() {
    return {
      id: ''
    }
  },
  components: {
    'v-article': article
  },
  computed: {
    ...mapState('movie', ['currentMovie'])
  },
  methods: {
    ...mapActions('movie', ['getMovieDetail', 'clearMovieDetail']),
    async initPage(id) {
      await this.getMovieDetail(id)
    }
  }
}
</script>

<style scoped>

</style>
