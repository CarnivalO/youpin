<template>
  <div>
    <mt-loadmore :top-method="loadTop" @top-status-change="handleTopChange">
      <ul>
        <li>
          <div class="listHeader">
            <img class="avatar" src="../assets/raw_1495871170.jpeg" />
            <span class="username">昵称昵称</span>
            <span class="postTime">1小时</span>
          </div>
          <div class="listBody">
            <p class="content">
              #美物推荐#YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看YSL好看好看真好看
              <a href="#">查看详情</a>
            </p>
            <img class="contentImg" src="https://modao.cc/uploads3/images/1015/10155658/raw_1496978376.jpeg" />
          </div>
          <div class="listFooter">
            <button class="like listButton" @click="like()">点赞
              <span class="likeCount">{{likeCount}}</span>
            </button>
            <button class="buy listButton">购买</button>
          </div>
        </li>
      </ul>
      <div slot="top" class="mint-loadmore-top">
        <span v-show="topStatus !== 'loading'" :class="{ 'rotate': topStatus === 'drop' }">↓</span>
        <span v-show="topStatus === 'loading'">Loading...</span>
      </div>
    </mt-loadmore>
  </div>
</template>

<script>
import axios from 'axios'
import { Loadmore } from 'mint-ui'

export default {
  data () {
    return {
      likeStatus: true,
      likeCount: 0,
      list: [],
      topStatus: ''
    }
  },
  methods: {
    handleTopChange (status) {
      this.topStatus = status
    },
    loadTop: {},
    like: function () {
      if (this.likeStatus) {
        this.likeStatus = !this.likeStatus
        this.likeCount++
      } else {
        this.likeStatus = !this.likeStatus
        this.likeCount--
      }
    },
    created () {
      axios.get('http://www.easy-mock.com/mock/593c185c8ac26d795fd2a68a/youpin/getImgs')
        .then(response => {
          console.log(response)
          this.imgs = response.data
        })
        .catch(error => {
          console.log(error)
          alert('网络错误，不能访问')
        })
    },
    components: {
      Loadmore
    }
  }
}
</script>

<style scoped>
a {
  text-decoration: none;
}

.listHeader {
  margin: 0 0 0.3em 0;
  height: 2em;
}

.avatar {
  height: 2em;
  width: 2em;
  float: left;
  margin: 0 0.6em 0 1em;
}

.username {
  float: left;
  line-height: 2.2em;
}

.postTime {
  float: right;
  line-height: 2.6em;
  color: #B5B5B5;
  margin: 0 2em;
  font-size: 0.9em;
}

.listBody {
  background: #F0F0F2;
}

.content {
  text-align: left;
}

.contentImg {
  width: 20em;
  height: 20em;
}

.listFooter {
  display: inline;
}

.listButton {
  background: #FFF;
  border: 1px solid #B2B2B2;
  width: 50%;
  height: 3em;
  float: left;
}
</style>
