<template>
  <div @click="clickHandle">
    <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <img class="userinfo-avatar" src="/static/images/user.png" background-size="cover" />

      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <div v-if="!isLogin">
      <Button type="primary" style="width: max-content;" @click="login">请登录</Button>
    </div>

    <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>
  </div>
</template>

<script>

import Vue from 'vue'
import card from '@/components/card'
import Button from 'vant/lib/button/index'
import mpvue from 'mpvue'

export default {
  data() {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: '未登录',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      },
      isLogin: false
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap() {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle(ev) {
      console.log('clickHandle:', ev)
    },
    login(ev) {
      console.log('login:', ev)
      wx.getUserProfile({
      desc: '用于完善会员资料', // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
      success: (res) => {
        this.userInfo = res.userInfo,
        this.isLogin = true
      }
    })
    }
  },

  created() {
    // let app = getApp()
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

a {
  padding: 10px;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.userlogin-button {
  width: min-content;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin: 20px;
  margin-bottom: 5px;
  border: 1px solid #8a8484;
}

.all {
  width: 7.5rem;
  height: 1rem;
  background-color: blue;
}

.all:after {
  display: block;
  content: '';
  clear: both;
}

.left {
  float: left;
  width: 3rem;
  height: 1rem;
  background-color: red;
}

.counter {
  float: right;
  margin-top: 200px;
  vertical-align: bottom;
}

.right {
  float: left;
  width: 4.5rem;
  height: 1rem;
  background-color: green;
}</style>
