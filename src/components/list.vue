<template>
  <div>
    <mt-loadmore :top-method="loadTop" @top-status-change="handleTopChange">
      <ul>
        <li v-for="(list,index) in lists" :key="list.id">
          <div class="listHeader">
            <img class="avatar" :src="list.avatar" />
            <span class="username">{{list.username}}</span>
            <span class="postTime">{{list.postTime}}</span>
          </div>
          <div class="listBody">
            <p class="content">
              {{list.content}}
              <a :href="list.detail">查看详情</a>
            </p>
            <img v-for="img1 in list.contentImgs" :src="img1" />
            <div class="clear"></div>
          </div>
          <div class="listFooter">
            <button class="like listButton" @click="like(index)">点赞
              <span class="likeCount">{{likes[index].likeCount}}</span>
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
  name: 'List',
  data() {
    return {
      lists: [],
      likes: [],
      topStatus: ''
    }
  },
  created() {
    axios.get('http://www.easy-mock.com/mock/593c185c8ac26d795fd2a68a/youpin/getList')
      .then(response => {
        this.lists = response.data
        for (let x in response.data) {
          let obj = {
            'likeStatus': false,
            'likeCount': response.data[x].likeCount
          }
          this.likes.push(obj)
        }
      })
      .catch(error => {
        console.log(error)
        alert('网络错误，不能访问')
      })
  },
  methods: {
    handleTopChange(status) {
      this.topStatus = status
    },
    loadTop: {},
    like: function (index) {
      if (this.likes[index].likeStatus) {
        this.likes[index].likeStatus = !this.likes[index].likeStatus
        this.likes[index].likeCount--
      } else {
        this.likes[index].likeStatus = !this.likes[index].likeStatus
        this.likes[index].likeCount++
      }
    },
    components: {
      'mt-loadmore': Loadmore
    }
  }
}
</script>

<style scoped>
a {
  text-decoration: none;
  color: #A86500;
}

.clear {
  clear: both;
  height: 0px;
}

.listHeader {
  margin: 0.3em 0 0.3em 0;
  height: 2em;
  clear: both;
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
  margin: 0 0.6em 0.6em 0.6em;
  text-align: left;
}

.listBody img {
  width: 48%;
  height: 48%;
  float: left;
  margin: 1%;
}

.listFooter {
  clear: both;
}

.listButton {
  background: #FFF;
  border: 1px solid #B2B2B2;
  width: 50%;
  height: 3em;
  float: left;
}
</style>
