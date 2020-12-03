<template>
  <view class="container">
      <view v-for="(card, index) in cards" :key="index" class="cards">
        <text class="title">{{ card.title }}</text>
        <image :src="card.bgImg" class="cover"/>
        <text>{{ card.content }}</text>
      </view>
  </view>
</template>

<script>
export default {
  data(){
    return{
		title: 'hello',
		cards: []
    };
  },
  onLoad() {
	  uni.request({
		  url: 'http://localhost:8080/api/cards',
		  success: res => {
			  console.log(res.data.data);
			  this.cards = res.data.data;
		  }
	  });
  },
  methods: {},
  };
</script>

<style scoped>

@font-face {
	font-family:'hot-nijia';
	src: url(../../fonts/HOT-Ninja Std R.otf);
}

.container {
  width: 600rpx;
  padding: 10rpx 10rpx;
}

.cards {
	font-family: 'hot-nijia';
	font-size: 18px;
  height: 500rpx;
  background-color: #CCCCCC;
  padding: 20rpx;
  border-radius: 10rpx;
  margin-bottom: 20rpx;
}

.title {
	font-size: 36rpx;
}

.cover {
  width: 500rpx;
  height: 300rpx;
  border-radius: 10rpx;
}

</style>