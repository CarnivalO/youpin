<template>
  <div class="page-swipe">
    <mt-header title="优品">
      <mt-button icon="more" slot="right"></mt-button>
    </mt-header>
    <mt-swipe :auto="4000">
      <mt-swipe-item v-for="image in images" :key="image.id">
        <img :src="image.url">
      </mt-swipe-item>
    </mt-swipe>
  
  </div>
</template>

<script>
import axios from 'axios'
import { Header, Swipe, SwipeItem } from 'mint-ui'

export default {
  name: 'Swipe',
  created () {
    axios.get('http://www.easy-mock.com/mock/593c185c8ac26d795fd2a68a/youpin/getImgs')
      .then(response => {
        this.images = response.data
      })
      .catch(error => {
        console.log(error)
        alert('网络错误，不能访问')
      })
  },
  data () {
    return {
      images: []
    }
  },
  components: {
    'mt-swipe': Swipe,
    'mt-swipe-item': SwipeItem,
    'mt-header': Header
  }
}

</script>

<style scoped>
.mint-swipe {
  height: 200px;
  text-align: center;
}

.mint-swipe img {
  width: 100%;
}
</style>
