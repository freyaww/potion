<template>
  <div class="container" @click="clickHandle('test click', $event)">
    <div class="enname-content">{{data.enname}}</div>
    <div class="cnname-content">{{data.cnname}}</div>
    <div class="img-content">
      <img :src="perfumeImg" alt="">
    </div>
    <div class="inf-content">
      <div class="inf-control">
        <span class="label-control">品牌：</span>
        <span class="detail-control">{{data.brand}}</span>
      </div>
      <div class="inf-control">
        <span class="label-control">香调：</span>
        <span class="detail-control">{{data.fragrance}}</span>
      </div>
      <div class="inf-control">
        <span class="label-control">前调：</span>
        <span class="detail-control"><span v-for="item in data.top" :key="item">{{item}}</span>&nbsp;</span>
      </div>
      <div class="inf-control">
        <span class="label-control">中调：</span>
        <span class="detail-control"><span v-for="item in data.middle" :key="item">{{item}}</span>&nbsp;</span>
      </div>
      <div class="inf-control">
        <span class="label-control">后调：</span>
        <span class="detail-control"><span v-for="item in data.base" :key="item">{{item}}</span>&nbsp;</span>
      </div>
      <div class="inf-control">
        <span class="label-control">属性：</span>
        <span class="detail-control">{{data.attrib}}</span>
      </div>
      <div class="inf-control">
        <span class="label-control">调香师：</span>
        <span class="detail-control">{{data.perfumer}}</span>
      </div>
    </div>
  </div>
</template>

<script>
  import card from '@/components/card'

  export default {
    data () {
      return {
        motto: 'Hello World',
        userInfo: {},
        data: {},
      }
    },
    computed: {
      perfumeImg () {
          return `https://img.xssdcdn.com/perfume/${this.data.id}.jpg`;
      },
    },
    components: {
      card
    },
    created () {
        let vm = this;
        console.log('created')
        wx.request({
          url: 'https://easy-mock.com/mock/5b1a0845b97c8172c435c424/getPotion',
          method: 'GET',
          success: function (data) {
            vm.data = data.data.data;
            console.log(vm.data);
          }
        })
    },
    methods: {
      bindViewTap () {
        const url = '../logs/main'
        wx.navigateTo({url})
      },
      getUserInfo () {
        // 调用登录接口
        wx.login({
          success: () => {
            wx.getUserInfo({
              success: (res) => {
                this.userInfo = res.userInfo
              }
            })
          }
        })
      },
      clickHandle (msg, ev) {
        console.log('clickHandle:', msg, ev)
      }
    },
  }
</script>

<style scoped>
  .container {
    display: flex;
    flex-flow: row wrap;
    justify-content: center;
  }
  .enname-content {
    padding: 20rpx;
    flex: 0 0 100%;
    font-weight: 700;
    text-align: center;
  }

  .cnname-content {
    padding: 20rpx;
    flex: 0 0 100%;
    font-family: Arial;
    font-weight: 700;
    text-align: center;
  }

  .img-content {
    margin: 40rpx auto;
    flex: 0 0 100%;
    text-align: center;
  }
  .img-content img {
    /*height: 50rpx;*/
    width: 300rpx;
  }

  .inf-content {
    padding-top: 30rpx;
    font-size: small;
    width: 500rpx;
    text-align: center;
  }

  .inf-control {
    display: flex;
  }

  .label-control {
    width: 150rpx;
    text-align: justify;
    padding: auto 20rpx;
  }

  .label-control:after {
    content: " ";
    display: inline-block;
    width: 100%;
  }

  .detail-control {

  }
</style>
