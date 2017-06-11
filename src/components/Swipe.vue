<template>
  <div class="page-swipe">
    <mt-swipe :auto="4000">
      <mt-swipe-item v-for="img in imgs"><img :src="img.url"></mt-swipe-item>
      </mt-swipe>
    
    </div>
</template>

<script>
import axios from 'axios'
import { Swipe, SwipeItem } from 'mint-ui'

export default {
  created () {
    axios.get('http://www.easy-mock.com/mock/593c185c8ac26d795fd2a68a/youpin/getImgs')
      .then(response => {
        this.imgs = response.data
      })
      .catch(error => {
        console.log(error)
        alert('网络错误，不能访问')
      })
  },
  data () {
    return {
      imgs: []
    }
  },
  components: {
    Swipe,
    SwipeItem
  }
}

</script>

<style scoped>
.mint-swipe {
  height: 200px;
  text-align: center;
}
.mint-swipe img{
  width: 100%;
}
</style>
