<template>
	<div class="header" :style="bg">
		<div class="top">
			<div class="top-back">
				<span class="icon-arrow_lift"></span>
			</div>
			<form class="top-search">
				<span class="search-icon"></span>
				<input class="search-bar" type="text" placeholder="商品搜尋">
			</form>
			<div class="top-more">
				<a href="#" class="spelling-btn">拼單</a>
				<div class="more-btn">
					<i class="s-radius"></i>
					<i class="s-radius"></i>
					<i class="s-radius"></i>
				</div>
			</div>
		</div>
		<div class="content">
			<div class="icon" :style="iconImg"></div>
			<div class="name">
				{{poiInfo.name}}
			</div>
			<div class="collect">
				<img src="./star.png">
				<span>收藏</span>
			</div>
		</div>
		<div class="bulletin" v-if="poiInfo.discounts2">
			<img :src="poiInfo.discounts2[0].icon_url">
			<span class="text">{{poiInfo.discounts2[0].info}}</span>
			<div class="detail" @click="bullentinOpen()">
				{{poiInfo.discounts2.length}}個活動
				<span class="icon-keyboard_arrow_right"></span>	
			</div>
		</div>
		<transition name="detail">
			<div class="bullentin-detail" v-show="isShow">
				<div class="info">
					<div class="main" :style="infoBg">
						<div class="icon" :style="iconImg"></div>
						<h3 class="name">{{poiInfo.name}}</h3>
						<div class="score">
							<star :score="poiInfo.wm_poi_score"></star>
							<span>{{poiInfo.wm_poi_score}}</span>
						</div>
						<p class="tip">
							{{poiInfo.min_price_tip}} <i>|</i>
							{{poiInfo.shipping_fee_tip}} <i>|</i>
							{{poiInfo.delivery_time_tip}}						
						</p>
						<p class="time">
							配送時間:
							{{poiInfo.shipping_time}}
						</p>
						<div class="discounts" v-if="poiInfo.discounts2">
							<p>
								<img :src="poiInfo.discounts2[0].icon_url">
								<span>{{poiInfo.discounts2[0].info}}</span>
							</p>
						</div>
					</div>
					<div class="close" @click="bullentinClose()">
						<span class="icon-close"></span>
					</div>
				</div>
			</div>
		</transition>
	</div>
</template>

<script>

import star from "@/components/star/star"
export default{
	data () {
		return{
			isShow: false,
		}
	},
	components: {
		star
	},
	props: {
		poiInfo: {
			type: Object,
			default: {}
		}
	},
	computed:{
		bg () {
			return "background-image: url("+this.poiInfo.head_pic_url+")"
		},
		iconImg () {
			return "background-image: url("+this.poiInfo.pic_url+")"
		},
		infoBg () {
			return "background-image: url("+this.poiInfo.poi_back_pic_url+")"
		}
	},
	methods:{
		bullentinOpen () {	
			this.isShow = true
		},
		bullentinClose () {
			this.isShow = false
		},

	}
}
</script>

<style lang="scss" scoped>
@import url("../../comm/style/icon.css");
@mixin size($w,$h:$w){
	width: $w;
	height: $h;
}
$color_white: white;
.header{
	@include size(100%,160px);
	padding-top: 20px;
	background-position: center 1px;
	background-size: 110% 126%;
	box-sizing: border-box;
}
.top{
	@include size(calc(100% - 36px),31px);
	margin: 6px 15px 0 21px;
	display: flex;
	justify-content: space-between;
	box-sizing: border-box;
	.top-back{
		@include size(50px,100%);
		text-align: center;
		line-height: 31px;
		color: $color_white;
	}
	.top-search{
		@include size(100%);
		margin-left: 21px;
		box-sizing: border-box;
		.search-icon{
			position: absolute;
			@include size(28px,31px);
			background: url('titans_h5_search@2x.png') no-repeat 11px center;
			background-size: 13px 13px;
		}
		.search-bar{
			border: none;
			@include size(100%);
			box-sizing: border-box;
			background-color: #cdcdcc;
			border-radius: 25px;
			padding-left: 28px;
			outline: none;
		}
	}
	.top-more{
		@include size(85px,25px);
		margin: 7px 0 0 24px;
		background-color: #000;
		display: flex;
		.spelling-btn{
			@include size(30px,17px);
			color: $color_white;
			line-height: 17px;
			border: 1px solid $color_white;
			text-align: center;
			float: left;
			text-decoration: none;
			font-size: 10px;
		}
		.more-btn{
			@include size(20px,24px);
			margin-left: 15px;
			margin-top: 7px;
			.s-radius{
				@include size(3px);
				border-radius: 50%;
				border: 1px solid $color_white;
				display: block;
				float: left;
				margin-right: 1px;
			}
		}
	}
}
.content{
	margin: 17px 10px 11px;
	@include size(100%,50px);
	box-sizing: border-box;
	display: flex;
	.icon{
		@include size(50px);
		background-size: 135% 100%;
		background-position: center;
		border-radius: 5px;
	}
	.name{
		height: 100%;
		padding: 18px 0 0 12px;
		font-size: 16px;
		font-weight: bold;
		color: $color_white;
	}
	.collect{
		@include size(25px,37px);
		position: absolute;
		right: 10px;
		text-align: center;
		img{
			@include size(20px);
			padding-top: 6px;
		}
		span{
			color: $color_white;
			font-size: 11px;
			margin-top: 7px;
		}
	}
}
.bulletin{
	margin: 0 10px;
	height: 16px;
	font-size: 11px;
	color: $color_white;
	white-space: nowrap;
	img{
		@include size(16px);
		margin-right: 6px;
		float: left;
	}
	.text{
		float: left;
		line-height: 16px;
	}
	.detail{
		float: right;
		cursor: pointer;
		span{
			font-size: 11px;
			line-height: 16px;
		}
	}
}
.bullentin-detail{
	@include size(100%);
	position: absolute;
	left: 0;
	top: 0;
	z-index: 999;
	background-color: rgba(98, 98, 98, 0.8);
}
.info{
	@include size(100%);
	padding: 43px 20px 125px;
	box-sizing: border-box;
}
.main{
	@include size(100%);
	background-size: 100% 100%;
	border-radius: 10px;
	text-align: center;
	.icon{
		@include size(60px);
		background-size: 135% 100%;
		background-position: center;
		border-radius: 5px;
		display: inline-block;
		margin-top: 40px;
	}
	.name{
		font-size: 15px;
		color: $color_white;
		margin-top: 13px;
		margin-bottom: 6px;
	}
	.score{
		height: 10px;
		line-height: 0;
		text-align: center;
		.star{
			display: inline-block;
			font-size: 0;
		}
		span{
			color: $color_white;
			margin-left: 4px;
		}
	}
	.tip{
		font-size: 11px;
		color: #bababc;
		margin-top: 8px;
		i{
			margin: 0 7px;
		}
	}
	.time{
		font-size: 11px;
		color: #bababc;
		margin-top: 13px;
	}
	.discounts{
		margin-top: 21px;
		padding: 0 20px;
		p{
			padding-top: 20px;
			border-top: 1px solid #bababc;			
			img{
				@include size(16px);
				vertical-align: middle;
				margin-right: 10px;
			}
			span{
				font-size:11px;
				line-height: 16px;
				color: $color_white;
			}
		}
	}
}
.close{
	@include size(40px);
	margin: 20px auto 65px;	
	border-radius: 50%;
	border: 1px solid rgba(140,140,140,0.9);
	background-color: rgba(118,118,118,0.7);
	text-align: center;
	cursor: pointer;
	span{		
		font-size: 14px;
		line-height: 40px;
		color: $color_white;
	}
}

.detail-enter-active, .detail-leave-active{
  transition: opacity 1s;
}
.detail-enter, .detail-leave-to{
  opacity: 0;
}	
</style>
