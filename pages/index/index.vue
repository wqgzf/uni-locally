<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,i) in imglist" :key="i">
				<image :src="item.image" mode="widthFix"></image>
			</swiper-item>
		</swiper>
				<uni-grid :column="3">
					<block v-for="(item,i) in namelist"  :key="i">
					<view @click="list(item.id)">
				    <uni-grid-item>
						<image class="icon" :src="item.icon" />
				        <text class="text">{{item.name}}</text>
				    </uni-grid-item>
					</view>
					</block>
				</uni-grid>
			
		<view>
			<image class="tu1" mode="widthFix" src="../../tu/images/link-01.png"></image>
			<image class="tu2" mode="widthFix" src="../../tu/images/link-02.png"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imglist:[],
				namelist:[]
			}
		},
		onLoad() {
			this.imagelist();
			this.getlist();
		},
		methods: {
			list(id){
				console.log(id)
				uni.navigateTo({
					url:'/pages/list/list?id='+id
				})
			},
		imagelist(){
			uni.request({
				url:'https://locally.uieee.com/slides',
				success:res => {
					this.imglist=res.data
				}
			})
		},
		getlist(){
			uni.request({
				url:'https://locally.uieee.com/categories',
				success:res=>{
					this.namelist=res.data
				}
			})
		}
		}
	}
</script>

<style>
	.tu1{
		width: 150px;
		margin-left: 2px;
		margin-top: 5px;
	}
	.tu2{
		width: 150px;
		margin-left: 10px;
		margin-top: 5px;
	}
	.navig{
		width: 100%;
	}
	.text{
		margin-left: 23px;
		
	}
	.icon{
		width: 50px;
		height: 50px;
		margin-left: 22px;
		margin-top: 10px;
	}
</style>
