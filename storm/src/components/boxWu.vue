<template>
	<div class="boxWu">
		<ul class="boxList">
			<li class="boxDian" v-for="(item , index) in boxList" @click="next(index)"><span>{{item.item}}</span></li>
		</ul>
		<div>{{text}}</div>
		<div>计时:{{startTimeMin}}分{{startTimeMonth}}秒</div>
	</div>
</template>

<script>
	export default {
		name: 'HelloWorld',
		data() {
			return {
				boxList: [{
					item: '1',
					click: false,
				}, {
					item: '2',
					click: false,
				}, {
					item: '3',
					click: false,
				}, {
					item: '4',
					click: false,
				}, {
					item: '5',
					click: false,
				}, {
					item: '6',
					click: false,
				}, {
					item: '7',
					click: false,
				}, {
					item: '8',
					click: false,
				}, {
					item: ''
				}, ],
				nullIndex: 0, //获取为空的下标
				text:'',
				startTimeMin:0,
				startTimeMonth:0,
			}
		},
		mounted: function() {
			let _this = this;
			_this.$nextTick(function() {
				this.boxList.sort(function() {
					return(0.5 - Math.random());
				});
				this.load();
			});
		},
		methods: {
			load(){
				let _this=this;
				setInterval(function(){
					_this.startTimeMonth=_this.startTimeMonth+1;
					if(_this.startTimeMonth==60){
						_this.startTimeMonth=0;
						_this.startTimeMin=_this.startTimeMin+1;
					}
				},1000);
			},
			next(index) {
				for(var i = 0; i < this.boxList.length; i++) {
					if((index + 3 < 9) && (this.boxList[index + 3].item == '')) {
						this.boxList[index].click = true;
					}
					if((index - 3 > -1) && (this.boxList[index - 3].item == '')) {
						this.boxList[index].click = true;
					}
					if((index + 1 < 9) && (this.boxList[index + 1].item == '')) {
						this.boxList[index].click = true;
					}
					if((index - 1 > -1) && (this.boxList[index - 1].item == '')) {
						this.boxList[index].click = true;
					}
					if(this.boxList[index].click) {
						if(this.boxList[i].item == '') {
							this.boxList[i].item = this.boxList[index].item;
							this.boxList[index].item = '';
						}
					}
				}
				var lengthBox=this.boxList.length;
				var j=0;
				for(var i = 0; i < lengthBox-1; i++) {
					this.boxList[i].click = false;
					if(this.boxList[i].item==i){
						j+=1;
						if(j==lengthBox){
							this.text="获胜成功"
						}
					}
				}
				console.log(this.boxList);
			}

		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.boxDian {
		width: 33%;
		height: 33.3%;
		/*background: url(../assets/bkcBox.png) center no-repeat;*/
		border: 1px solid black;
		float: left;
		list-style: none;
		font-size: 60px;
		text-align: center;
	}
	
	.boxDian {
		display: flex;
	}
	
	.boxDian span {
		margin: auto;
	}
	
	.boxList {
		width: 700px;
		height: 700px;
	}
</style>