<script>
export default {
  mounted(){
    let userInfo = uni.getStorageSync('userInfo')
    if (!userInfo) {
            uni.navigateTo({
        url: '/pages/login/main'
      })
    }
  },
  methods: {

  }
}
</script>