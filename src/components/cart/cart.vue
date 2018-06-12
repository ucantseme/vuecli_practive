<template>
	<div class="shopcart" :class="{active:totalCount>0}">
		<div class="left">
			<div class="cart" :class="{active:totalCount>0}">
				<span class="icon-shopping_cart" :class="{active:totalCount>0}"></span>
				<i v-show="totalCount">{{totalCount}}</i>
			</div>
			<div class="desc">
				<h3 v-show="totalPrice">￥{{totalPrice}}</h3>
				<p :class="{active:totalCount>0}">{{shipping_fee_tip}}</p>
			</div>
		</div>
		<div class="right"  :class="{active:totalCount>0}">
			{{payBtn}}
		</div>
	</div>
</template>

<script>
	export default{
		props: {
			min_price_tip: {
				type: String,
				default: ''
			},
			shipping_fee_tip: {
				type: String,
				default: ''
			},
			selectFoods: {
				type: Array,
				default() {
					return [
						{
							min_price: 100,
							count: 2,
						},
						{
							min_price: 130,
							count: 3,
						}
					]
				}
			}
		},
		computed: {
			totalCount () {
				let num = 0;
				this.selectFoods.forEach( (food) => {
					num += food.count;
				})
				return num;
			},
			totalPrice () {
				let price = 0;
				this.selectFoods.forEach( (food) => {
					price += food.min_price * food.count;
				});
				return price;
			},
			payBtn () {
				if(this.totalCount > 0){
					return "去結算"
				} {
						return this.min_price_tip
					}
			}
		}
	}
</script>

<style lang="scss" scoped>
@import url("../../comm/style/icon.css");
$font_color: #bab9b9;
$active_black: #2d2b2a;
$active_yellow: #ffd161;
$white_color: #fff;
.shopcart{
	width: 100%;
	height: 51px;
	background-color: #514f4f;
	position: fixed;
	left: 0;
	bottom: 0;
	display: flex;
	&.active{
		background-color: $active_black;
	}
}
.left{
	flex: 1;
	.cart{
		width: 50px;
		height: 50px;
		background-color: #666666;
		border-radius: 50%;
		position: relative;
		top: -14px;
		left: 10px;
		text-align: center;
		float: left;
		&.active{
			background-color: #ffd161;
		}
		span{
			font-size: 28px;
			color: #c4c4c4;
			line-height: 50px;
			&.active{
				color: $active_black;
			}
		}
		i{
			width: 15px;
			height: 15px;
			line-height: 15px;
			border-radius: 50%;
			font-size: 9px;
			color: $white_color;
			background-color: red;
			position: absolute;
			right: 0;
			top: 0;
		}
	}
	.desc{
		float: left;
		margin-left: 13px;
		h3{
			font-size: 18px;
			line-height: 33px;
			color: $white_color;
		}
		p{
			font-size: 12px;
			color: $font_color;
			line-height: 50px;
			&.avtive{
				line-height: 12px;
			}
		}
	}
}
.right{
	flex: 0 0 110px;
	font-size: 15px;
	font-weight: bold;
	color: $font_color;
	line-height: 50px;
	text-align: center;
	&.active{
		background-color: $active_yellow;
		color: $active_black;
	}
}
</style>
