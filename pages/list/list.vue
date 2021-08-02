<template>
	<view>
		<uni-search-bar placeholder="请输入搜索内容" @confirm="search" @cancel="cancel" cancel-text="取消">
		    <uni-icons slot="searchIcon" color="#999999" size="18" type="home" />
		</uni-search-bar>
		<block v-for="(item,i) in lielist" :key="i">
			<view class="img">
				<image class="image" :src="item.images[0]"></image>
				<view class="name">{{item.name}}</view>
				<view class="dh">
					<view>
						电话:{{item.phone}}<br/>
						地址:{{item.address}}<br/>
						营业时间:{{item.businessHours}}
					</view>
				</view>
				<view class="xl">
					{{item.score}}
				</view>
			</view>
			
		</block>
		<uni-load-more :status="more"></uni-load-more>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				more:'more',
				id:'',
				_page:1,
				_limit:20,
				lielist:[],
				datt:0
			}
		},
		methods: {
			getlist(){
				this.more='loading'
				uni.request({
					url:`https://locally.uieee.com/categories/${this.id}/shops?_page=${this._page}&_limit=${this._limit}`,
					success:res=>{
						this.lielist=[...this.lielist,...res.data]
						// if(this.lielist.length==res.data.length)	
						if(res.data==''){
							this.more='more'
						}
					}
					
				})
				this.more="more"
			}
		},onLoad(op){
			this.id=op.id
			this.getlist();
		},onReachBottom(){
			this._page++;
			this.getlist();
			
		},onPullDownRefresh(){
			this.lielist=[]
			this.getlist();
			uni.stopPullDownRefresh();
		}
	}
</script>

<style>
	.xl{
		color: red;
		margin-left: 285px;
		margin-top: -80px;
	}
	.dh{
		font-size: 12px;
		margin-left: 100px;
	}
	.img{
		width: 100%;
		height: 110px;
		border: 1px solid black;
	}
.image{
	width: 100px;
	height: 100px;
}
.name{
	margin-left: 110px;
	margin-top: -105px;
}
</style>
