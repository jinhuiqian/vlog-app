<template>
	<view>
	<view class="mb-2 flex align-stretch">
	  <view class="border-bottom flex align-center justify-center font px-2">+86</view>
	  <input type="text" v-model="phone" placeholder="手机号" class="border-bottom p-2 flex-1" />
	</view>
	<view class="mb-2 flex align-stretch">
	  <input type="text" v-model="code" placeholder="请输入验证码" class="border-bottom p-2 flex-1" />
	  <view 
	    class="border-bottom flex align-center justify-center font-sm text-white"
	    :class="codeTime > 0 ? 'bg-main-disabled' : 'bg-main'"
	    style="width: 180rpx;"
	    @click="getCode"
	    >
	    {{ codeTime > 0 ? codeTime + ' s' : '获取验证码' }}
	  </view>
	</view>
	
	<view class="py-2 px-3">
		<button 
		class="bg-main text-white " 
		style="border-radius: 50rpx;border: 0;" 
		type="primary" 
		:disabled="disabled"
		:class="disabled ? 'bg-main-disabled' : 'bg-main'"
		@click="submit">
			完成
		</button>
		</view>
	</view>
</template>

<script>
	import uniStatusBar from '@/components/uni-ui/uni-status-bar/uni-status-bar.vue';
	export default {
		components: {
		  uniStatusBar
		},
		data() {
			return {
				phone: '',
				code: '',
				codeTime: 0,
				loading: false
			}
		},
		computed: {
		    disabled() {
		      if(this.phone === '' || this.code === '')
		  {
		    return true;
		  }
		  return false;
		    }
		  },
		methods: {
			//初始化表单
			initForm() {
			  this.phone = '';
			  this.code = '';
			},
			//获取验证码
			getCode(){
			  //防止重复获取
			  if(this.codeTime > 0){
			    return;
			  }
			  //验证手机号
			  if (!this.validate()) return;
			  //请求数据
			  this.$H
			    .post(
			      '/user/sendcode?phone='+this.phone,
			      {
			        native: true 
			      })
			    .then(res => {
			      //倒计时
			      this.codeTime = 60;
			      let timer = setInterval(() =>{
			        if(this.codeTime >= 1){
			          this.codeTime--;
			        }else{
			          this.codeTime = 0;
			          clearInterval(timer);
			        }
			      },1000);
			    });
			},
			//表单验证
			validate() {
			  //手机号正则
			  var mPattern = /^1[34578]\d{9}$/;
			  if(!mPattern.test(this.phone)) {
			    uni.showToast({
			      title: '手机格式不正确',
			      icon: 'none'
			    });
			    return false;
			  }
			  // ...更多验证
			  return true;
			},
			// 提交
			    submit() {
			        //手机验证码登录
			        if(!this.validate()) return;
			        url = '/user/bindphone';
			        data = {
			          phone: this.phone,
			          code: this.code
			        };
			      //提交后端
			      this.loading = true;
			      this.$H
			        .post(url,data)
			        .then(res => {
			          this.loading = false;
						if(res) {
			          console.log(res);
			          //修改vuex的state，持久化存储
			          this.$store.commit('login',res);
			          //提示和跳转
			          uni.showModal({
			            title: '登录成功',
			            content: '去看看',
			            success: function(res){
			              if(res.confirm){
			                uni.switchTab({
			                  url:'../my/my'
			                });
			              }else if(res.cancel){
			                console.log('用户点击取消');
			                return;
			              }
			            }
			          });
			        }else{
						  uni.showModal({
							  title: '登录失败'
						  });
						  return;
					  }
					 })
			        .catch(err => {
			          //登录失败
			          this.loading = false;
			        });
			    }
			  }
			};
</script>

<style>

</style>
