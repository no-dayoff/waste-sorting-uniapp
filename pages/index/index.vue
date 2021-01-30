<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<view>这里展示从数据库中获取的数据</view>
		<view>{{name}}</view>
		<view>{{category}}</view>
		<unicloud-db v-slot:default="{data, loading, error, options}" collection="trash" field="name" :getone="true" where="name=='阿司匹林'">
		  <view>
		    {{data}}
		  </view>
		</unicloud-db>
		<u-button type="primary">主要按钮</u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				name:"",
				category:"",
			}
		},
		onLoad() {
			// 获取db引用
			const db = uniCloud.database() //代码块为cdb
			  db.collection('trash')
			    .where('name == "阿司匹林"')
			    .get()
			    .then((res)=>{
				  this.name=res.result.data[0].name
				  this.category=res.result.data[0].category
			    }).catch((err)=>{
			      // err.message 错误信息
			      // err.code 错误码
			    })
		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
