<template>
	<view class="information">
		<!-- #ifdef MP-ALIPAY|MP-WEIXIN|H5 -->
		<view class="kong">
			<image src="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2680786358,1010619428&fm=26&gp=0.jpg" mode="widthFix"
			 class="bgc" :style="{'display':bao==0?'block':'none'}"></image>
			<text :style="{'display':bao==0?'block':'none'}">空空滴，还没有记录</text>
			<text :style="{'display':bao==0?'block':'none'}">~快去选本书~</text>
		</view>
		<!-- #endif -->
		<view class="cont" v-for="item in bao" :key="item.id">
			<view class="img">
				<image :src="`https://uptownlet.com/appendix/image.jspx?id=${item.tp}`"></image>
			</view>
			<view class="jianjie">
				<text class="tit">{{item.bt}}</text>
				<text class="name"><text class="red zuozhe">作者:</text>{{item.zz}}</text>
				<view class="hot">
					<text class="text"><text class="iconfont icon-huo"></text>{{item.zxrd}}</text>
				</view>
				<!-- <view class="hide1" style="font-size: 15px;">{{item.bt}}</view>
				<view class="hide jj" >{{item.zy}}</view>
				<view style="font-size: 13px; color: #969896;" class="hide1">
					{{item.data.ly}}
				</view> -->
				
			</view>
			<view class="jiaru">
				<view class="s-bottom" @click="jiabao(item.id,item)">
					<text class="iconfont icon-shanchu" ></text>
					<text>删除</text>
				</view>
			</view>
		</view>
		<view class="foot">
			<view class="foot-center">
				<view class="zanbu">
					暂不可借阅
				</view>
				<view class="jieshu">
					借书
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import {
		mapState
	} from 'vuex';
	import {
		mapMutations
	} from 'vuex'
	export default {
		data() {
			return {
			}
		},
		computed: {
			
			...mapState({
				bao: 'bao'
			}),
			...mapState({
				carts: 'carts'
			})
		},
		
		methods: {
			...mapMutations({
				clearCarts: "clearCarts"
			}),
			...mapMutations({
				clearBao: "clearBao"
			}),
			...mapMutations({
				addCarts: "addCarts"
			}),
			shoucang(id, item) {
				if(item.sc==true){
					this.clearCarts(item)
					item.sc=false
				}else{
					this.addCarts(item)
					item.sc=true
				}
			},
			jiabao(id, item) {
				this.clearBao(item)
			}
		}
	}
</script>

<style lang="scss">
	page {
		/* #ifdef MP-ALIPAY */
		background-color: #fff;
		/* #endif */
	}

	.information {
		.kong {
			display: flex;
			flex-direction: column;

			.bgc {
				margin-top: 65px;
				margin-bottom: 10px;
			}

			text {
				text-align: center;
				font-size: 14px;
				color: #999;
				line-height: 25px;
			}

			text:nth-child(2) {
				font-size: 12px;
			}
		}

		.red {
			color: red;
		}

		width: 100%;
		padding: 0 20rpx;
		box-sizing: border-box;

		.cont {
			display: flex;
			justify-content: space-between;
			padding: 10rpx 0;
			border-bottom: 1px solid #eee;

			.img {
				image {
					width: 110rpx;
					height: 140rpx;
				}
			}

			.jianjie {
				display: flex;
				flex-direction: column;
				justify-content: space-around;
				width: 220px;
				box-sizing: border-box;
				padding: 13rpx 0;

				.tit {
					font-size: 14px;
					color: #333333;
					white-space: nowrap;
					overflow: hidden;
					text-overflow: ellipsis;
				}

				.name {
					font-size: 12px;
					color: #666666;

					.zuozhe {
						margin-right: 4rpx;
					}
				}

				.hot {
					font-size: 11px;
					color: #666666;
					margin-left: 20rpx;

					.icon-huo {
						color: #ef7302;
						font-size: 10px;
						margin-right: 3px;
					}
				}
			}

			.jiaru {
				width: 90rpx; // background-color: pink;
				text-align: center;
				font-size: 11px;
				border-left: 1px dashed #eee;
				padding-left: 10px;
				color: #808080;
				display: flex;
				flex-direction: column;
				justify-content: center;
				.s-bottom {
					display: flex;
					flex-direction: column;
					
				}
			}


		}
		.foot{
			width: 100%;
			// height: 50px;
			// background-color: pink;
			position: fixed;
            bottom:20px;
			padding: 0;
			left: 0;
			.foot-center{
				display: flex;
				justify-content: center;
				width:280px;
				margin: 0 auto;
				border-radius: 20px;
				border: 1px solid #eee;
				.zanbu{
					// background-color: red;
					width: 140px;
					text-align: center;
					color: #19CAAD;
					font-size: 13px;
					padding: 8px 0;
					border-top-left-radius: 20px;
					border-bottom-left-radius: 20px;
				}
				.jieshu{
					background-color:  #19CAAD;
					width: 140px;
					text-align: center;
					color: #fff;
					font-size: 13px;
					padding: 8px 0;
					border-top-right-radius: 20px;
					border-bottom-right-radius: 20px;
				}
			}
		}

	}
</style>
