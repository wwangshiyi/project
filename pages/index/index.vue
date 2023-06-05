<template>
	<view class="content">
		<view class="box">
			<view class="topBox">
				<uni-icons type="calendar-filled" size="20" id="icon" color="#38c882"></uni-icons>
				<text class="name">次卡名称</text>
				<text class="num">剩余&nbsp;99次</text>
			</view>
			<view class="centreBox">每次可兑换任意一份商品</view>
			<view class="bottomBox">￥<text class="number">33</text>.25/次
				<button size="mini" style="float: right;background-color: #3bc880;color: aliceblue;border-radius: 40rpx;">立即购买</button>
			</view>
		</view>
		<view class="dayBox">
			<scroll-view scroll-x="true">
				<block v-for="(item, index) in dayList" :key="index">
					<view class="dayTitle" :class="current == index ? 'select' : ''" @click="timeSelectd(index)">
						<view style="display: flex;flex-direction: column;justify-content: center;width: 100%;height: 100%;">
							<view>{{ item.day }}</view>
							<view v-if="index == 0" style="font-size: 25rpx;">今天</view>
							<view v-else style="font-size: 25rpx;">星期{{ item.week }}</view>
						</view>
					</view>
				</block>
			</scroll-view>
		</view>
	<view class="maxBox" v-if="current===0">
		<view class="substance" v-for="item,index in matter" :key="index">
			  <image :src="item.image" alt="" class="imageFir" ></image>
			<view class="small">
				<view class="text">{{item.text}}</view>
				<text class="labelOne">{{item.labelOne}}</text>
				<text class="labelOne labelTwo">{{item.labelTwo}}</text>
				<text class="labelOne labelTwo">{{item.labelThree}}</text>
			<view style="margin-top: 30rpx;">
				<text class="figure">{{item.sprice}}</text>
				<text class="explain">{{item.explain}}</text>
				<button size="mini" style="float: right;background-color: #3bc880;
				color: aliceblue;border-radius: 40rpx;margin-right: 30rpx;margin-top: -10rpx;
				" @click.native="addData(item.number)">{{item.number}}</button>
			   </view>	 
			 </view>
			</view>
			<view class="tip">
				<text class="lineOne"></text> 
				<text class="bottomTxt">{{tip}}</text>
				<text class="lineTwo"></text>
				</view>
		</view>
		<view class="maxBox" v-if="current===1">
			<img src="../../static/previewFix (1).jpg" alt="" style="margin-left: 100rpx;width: 500rpx;height: 500rpx;">
		</view>
	</view>
</template>
<script>
	import common from "../../common .js" 
	export default {
		data() {
			return {
				isShow: false,
				current: 0,
				dayList: [],
				xzTime: common.GetNowTime(new Date()),
				tip:"到底了",
				total:4,
				matter:[
					{
					image:require("../../static/previewFix.jpg"),
					text:"模拟假数据",
					labelOne:"好看图片",
					labelTwo:"商品名称",
					labelThree:"商品标签",
					sprice:"￥45",
					explain:"可用此卡兑换",
					number:"预定",
					num:"1"
				},
				{
					image:require("../../static/previewFix (1).jpg"),
					text:"假数据",
					labelOne:"好看图片",
					labelTwo:"商品名称",
					labelThree:"商品标签",
					sprice:"￥105",
					explain:"可用此卡兑换",
					number:"预订",
					num:"2"
				},
			  ]
			}
		},
		onLoad() {
			this.dayList = common.weekDate().dayList;
		},
		methods: {
			// 日期选择
			timeSelectd(index) {
				this.current = index;
				let date = this.dayList[index].year + '-' + this.dayList[index].month + '-' + this.dayList[index].day;
				date = common.GetNowTime(new Date(date));
				this.xzTime = date;
			},
			addData(num){
				if(num==="预定"){
					this.matter.push({
						image:require("../../static/previewFix.jpg"),
						text:"模拟假数据",
						labelOne:"好看图片",
						labelTwo:"商品名称",
						labelThree:"商品标签",
						sprice:"￥45",
						explain:"可用此卡兑换",
						number:"预定",
					})
				}
				if(num==="预订"){
					this.matter.push({
						image:require("../../static/previewFix (1).jpg"),
						text:"假数据",
						labelOne:"好看图片",
						labelTwo:"商品名称",
						labelThree:"商品标签",
						sprice:"￥105",
						explain:"可用此卡兑换",
						number:"预订",
					})
				}
			},
		}
	}
</script>

<style scoped>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.box{
		width: 700rpx;
		height: 230rpx;
		margin-top: 20rpx;
		border-radius: 30rpx;
		background-color: black;
	}
	.topBox{
		width: 670rpx;
		height: 60rpx;
		margin: 20rpx 20rpx 0 20rpx;
	}
	#icon{
		width: 50rpx;
		height: 50rpx;
	}
	.name{
		width: 50rpx;
		height: 50rpx;
		position: relative;
		top: -4rpx;
		left: 8rpx;
		color: white;
	}
	.num{
		float: right;
		margin-right: 6rpx;
		color: #368864;
	}
	.centreBox{
		font-size: 24rpx;
		color: gray;
		margin-left: 24rpx;
	}
	.bottomBox{
		width: 670rpx;
		height: 80rpx;
		margin: 34rpx auto;
		line-height: 80rpx;
		font-size: 24rpx;
		color: aliceblue;
	}
	.number{
		font-size: 36rpx;
	}
	/* 日期的渲染 */
	.dayBox{
		width: 700rpx;
		height: 160rpx;
		margin-top: 20rpx;
		display: flex;
		white-space: nowrap;
	}
	scroll-view {
		padding: 20upx 0;
		width: 100%;
		white-space: nowrap;
	}
	.dayTitle {
		width: 120rpx;
		height: 120rpx;
		border-radius: 60upx;
		margin-left: 20upx;
		text-align: center;
		display: inline-block;
	}
	.select {
		color: #ffffff;
		background-color: #83cbac;
	}
	.maxBox{
		width: 100vw;
		height: 100vh;
		background-color: #f6f6f6;
	}
	.substance{
		width: 700rpx;
		height: 200rpx;
		margin: 20rpx auto;
		background-color: white;
		border-radius: 20rpx;
	}
	.imageFir{
		width: 160rpx;
		height: 130rpx;
		border-radius: 20rpx;
		line-height: 130rpx;
		float: left;
		margin: 35rpx 0 10rpx 20rpx;
	}
	.small{
		width: 500rpx;
		height: 130rpx;
		float: right;
		margin: 30rpx 0 0 20rpx;
	}
	.text{
		font-size: 28rpx;
		font-weight: 700;
	}
	.labelOne{
		width: 40rpx;
		height: 30rpx;
		font-size: 24rpx;
		color: #3dc782;
		border: 1px solid #3dc782;
	}
	.labelTwo{
		color: gray;
		border: 1px solid gray;
		margin-left: 30rpx;
	}
	.figure{
		font-size: 28rpx;
		color: #ea8275;
	}
	.explain{
		color: gray;
		font-size: 24rpx;
		margin-left: 20rpx;
	}
	.lineOne{
		width: 50rpx;
		height: 1rpx;
		opacity: 0.5;
		display: inline-block;
		border-top: solid gray;
	}
	.tip{
		font-size: 24rpx;
		color: gray;
		width: 46%;
		margin-left: 40%;
		opacity: 0.5;
	}
	.bottomTxt{
		position: relative;
		top: 3rpx;
	}
	.lineTwo{
		width: 50rpx;
		height: 1rpx;
		display: inline-block;
		border-top: solid gray;
		opacity: 0.5;
	}
</style>
