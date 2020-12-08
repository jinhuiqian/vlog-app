<template>
	<view>
	<view>
		 <uni-list-item title="修改密码" @click="open('user-password')"></uni-list-item>
		 <uni-list-item title="绑定手机" @click="open()"></uni-list-item>
		 <uni-list-item title="绑定微信" @click="open()"></uni-list-item>
		 <uni-list-item title="绑定QQ" @click="open()"></uni-list-item>
	</view>
	
	
	</view>
</template>

<script>
	import uniListItem from '@/components/uni-ui/uni-list-item/uni-list-item.vue';
	export default {
		components:{
		  uniListItem
		},
		data() {
			
		},
		onLoad() {
		  
		},
		methods: {
			open(path) {
			  uni.navigateTo({
			    url: `../${path}/${path}`
			  });
		}
	}
}
</script>

<style>

</style>
