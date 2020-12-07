<template>
	<view>
		<view class="flex justify-center">
			<image src="../../static/me.jpg" style="border-radius: 50%;width: 200rpx;height: 200rpx; ;"></image>
		</view>
		
		<view class=" text-secondary flex justify-center m-2">version 1.0.0</view>
	
		<view>
		<uni-list-item title="新版本检测" @click="open()"></uni-list-item>
		<uni-list-item title="社区用户协议" @click="open()"></uni-list-item>
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
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
