<template>
	<div class="goods">
		<div class="menu" ref="menuScroll">
			<ul>
				<li class="menu-item" :class="{active:rightMenu===0}" @click="clickMenu(0)">
					<p class="text">
						<img :src="operation.tag_icon" v-if="operation.tag_icon" class="icon">
						{{operation.tag_name}}
					</p>
				</li>
				<li class="menu-item" v-for="(item,id) in goods" :class="{active:rightMenu===id+1}" @click="clickMenu(id+1)">
					<p class="text">
						<img :src="item.icon" v-if="item.icon" class="icon">
						{{item.name}}
					</p>
				</li>
			</ul>
		</div>
		<div class="foods" ref="foodScroll">
			<ul>
				<div class="operation-list list-hook">
					<div v-for="item in operation.operation_source_list">
						<img :src="item.pic_url">
					</div>
				</div>
				<li class="food-list list-hook" v-for="item in goods">
					<h3 class="title">{{item.name}}</h3>
					<ul>
						<li class="food-item" v-for="food in item.spus">
							<div class="icon" :style="itemIcon(food.picture)"></div>
							<div class="content">
								<h3 class="name">{{food.name}}</h3>
								<p class="desc" v-if="food.description">{{food.description}}</p>
								<div class="extra">
									<span class="saled">{{food.month_saled_content}}</span>
									<span class="praise">{{food.praise_content}}</span>
								</div>
								<img class="product" :src="food.product_label_picture">
								<p class="price">
									<span class="text">￥{{food.min_price}}</span>
									<span class="unit">/{{food.unit}}</span>
								</p>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
		<shopcart :shipping_fee_tip="poiInfo.shipping_fee_tip" :min_price_tip="poiInfo.min_price_tip"></shopcart>
	</div>
</template>

<script>
import BScroll from 'better-scroll'
import shopcart from '@/components/cart/cart'
export default {
  data() {
    return {
      operation: {},
			goods: {},
			poiInfo: {},
			listH: [],
			scrollY: 0,
			menuScroll: {},
			foodScroll: {},
    };
	},
	components: {
		shopcart,
	},
  created() {
    let vm = this;
    this.$axios
      .get("/api/goods")
      .then(function(res) {
        let dataSource = res.data;
        if (dataSource.code == 0) {
          vm.operation = dataSource.data.container_operation_source;
					vm.goods = dataSource.data.food_spu_tags;
					vm.poiInfo = dataSource.data.poi_info;
					vm.$nextTick(()=>{
						vm.scroll();
						vm.calcH();						
						})
        }
      })
      .catch(function(err) {
        console.log(err);
      });
	},
  methods: {
    itemIcon (id) {
      return "background-image: url(" + id + ")";
		},
		scroll () {
			this.menuScroll = new BScroll(this.$refs.menuScroll, {
				click: true
			});
			this.foodScroll = new BScroll(this.$refs.foodScroll, {
				probeType: 3
			});
			this.foodScroll.on('scroll', (pos) => {
				this.scrollY = Math.abs(Math.round(pos.y))
			})
		},
		calcH () {
			let foodlist = this.$refs.foodScroll.getElementsByClassName('list-hook');
			let height = 0;
			this.listH.push(height);
			for(let i=0;i<foodlist.length;i++){
				let item = foodlist[i];

				height += item.clientHeight;
				this.listH.push(height);
			}
		},
		clickMenu (id) {
			let foodlist = this.$refs.foodScroll.getElementsByClassName('list-hook');
			let el = foodlist[id];
			this.foodScroll.scrollToElement(el, 250)
		}
	},
	computed: {
		rightMenu () {
			for(let i=0;i<this.listH.length;i++){
				let height1 = this.listH[i];
				let height2 = this.listH[i+1];

				if(this.scrollY>=height1 && this.scrollY<height2){
					return i;
				}
			}
			return 0
		},

	}
};
</script>

<style lang="scss" scoped>
$border_color: #e4e4e4;
$name_color: #333333;
$content_font_color: #bfbfbf;

.goods {
  display: flex;
  position: absolute;
  top: 200px;
  bottom: 51px;
  overflow: hidden;
  width: 100%;
}
.menu {
  flex: 0 0 85px;
	background-color: #f4f4f4;
}
.menu-item {
  list-style: none;
  padding: 16px 23px 15px 10px;
	border-bottom: 1px solid $border_color;
	&.active{
		background-color: white;
		font-weight: bold;
		margin-top: -1px;
	}
  .text {
    color: $name_color;
    font-size: 13px;
    line-height: 17px;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  img {
    width: 15px;
    height: 15px;
    vertical-align: middle;
  }
}
.foods {
	flex: 1;
}
.operation-list{
	padding: 11px 11px 0 11px;
	border-bottom: 1px solid $border_color;
	img{
		width: 100%;
		margin-bottom: 11px;
		border-radius: 5px;
	}
}
.food-list{
	padding: 11px;
	.title{
		height: 13px;
		font-size: 13px;
		background: url("btn_yellow_highlighted@2x.png") no-repeat left center;
		background-size: 2px 10px;
		padding-left: 7px;
		margin-bottom: 12px;
	}
}
.food-item{
	display: flex;
	margin-bottom: 25px;
	.icon{
		height: 75px;
		flex: 0 0 63px;
		background-position: center;
		background-size: 120% 100%;
		background-repeat: no-repeat;
		margin-right: 11px;
	}
	.content{
		flex: 1;
	}
}
.content{
	.name{
		font-size: 16px;
		line-height: 21px;
		color: $name_color;
		margin-bottom: 10px;
		padding-right: 27px;
	}
	.desc{
		font-size: 10px;
		line-height: 19px;
		color: $content_font_color;
		margin-bottom: 8px;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 1;
		overflow: hidden;
	}
	.extra{
		font-size: 10px;
		color: $content_font_color;
		margin-bottom: 7px;
		.saled{

			margin-right: 14px;
		}
	}
	.product{
		height: 15px;
		margin-bottom: 6px;
	}
	.price{
		font-size: 0px;
		.text{
			font-size: 14px;
			color: #fb4e44;
		}
		.unit{
			font-size: 12px;
			color: $content_font_color;
		}
	}
}



</style>
