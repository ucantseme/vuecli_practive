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
				<img src="../../../resource/img/star.png">
				<span>收藏</span>
			</div>
		</div>
		<div class="bulletin">

		</div>
	</div>
</template>

<script>
export default{
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
		}
	}
}
</script>

<style lang="scss" scoped>
@import url("../../comm/style/icon.css");
@mixin size($w,$h:$w){
	width: $w;
	height: $h;
}
.header{
	height: 160px;
	padding-top: 20px;
	background-position: center 1px;
	background-size: 110% 126%;
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
		color: white;
	}
	.top-search{
		@include size(100%);
		margin-left: 21px;
		box-sizing: border-box;
		.search-icon{
			position: absolute;
			@include size(28px,31px);
			background: url('../../../resource/img/titans_h5_search@2x.png') no-repeat 11px center;
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
			color: white;
			line-height: 17px;
			border: 1px solid white;
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
				border: 1px solid white;
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
		color: white;
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
			color: white;
			font-size: 11px;
			margin-top: 7px;
		}
	}
}
	
</style>
