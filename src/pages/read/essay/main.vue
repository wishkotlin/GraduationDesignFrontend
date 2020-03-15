<template>
  <div>
    <v-article
      :title="readContent.essay.hp_title"
      :user_name="readContent.essay.hp_author"
      :content="readContent.essay.hp_content"
    ></v-article>
  </div>
</template>

<script>
import article from '@/components/article'
import { mapState, mapActions } from 'vuex'
export default {
  onLoad(params) {
    this.clearReadContent({type: 'essay'})
    const { id } = params
    this.getReadContent({ type: 'essay', id })
	console.log(this.readContent, "readContent")
  },
  components: {
    'v-article': article
  },
  computed: {
    ...mapState('read', ['readContent'])
  },
  methods: {
    ...mapActions('read', ['getReadContent', 'clearReadContent'])
  }
}
</script>

<style scoped>

</style>
