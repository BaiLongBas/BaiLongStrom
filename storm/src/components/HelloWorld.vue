<template>
	<div class="hello">
		<ul class="bodyUl">
			<li v-for="(item,index) in  dataPas" @click="liClick(index)">
				<div v-if="item.paseIne!=''&&item.paseIne=='radio'" class="radio"></div>
				<div v-else-if="item.paseIne!=''&&item.paseIne=='cha'" class="cha"></div>
			</li>
		</ul>
		<div class="rightTextBut">
			{{textList}}<br /><br />
			<button @click="clearLine">清空棋盘</button><br /><br />
			<button @click="start">开始游戏</button><br /><br />
			<span>游戏状态:{{stromType}}</span>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'HelloWorld',
		data() {
			return {
				dataPas: [{
					paseIne: '',
					dataType: false,
					index: '0'
				}, {
					paseIne: '',
					dataType: false,
					index: '1'
				}, {
					paseIne: '',
					dataType: false,
					index: '2'
				}, {
					paseIne: '',
					dataType: false,
					index: '3'
				}, {
					paseIne: '',
					dataType: false,
					index: '4'
				}, {
					paseIne: '',
					dataType: false,
					index: '5'
				}, {
					paseIne: '',
					dataType: false,
					index: '6'
				}, {
					paseIne: '',
					dataType: false,
					index: '7'
				}, {
					paseIne: '',
					dataType: false,
					index: '8'
				}],
				dataPasBas: [],
				dateLength: 0,
				textList: '',
				stromType: '',
			}
		},
		mounted: function() {
			let _this = this;
			_this.$nextTick(function() {
				var dataPasBas = this.dataPas;
				this.dataPasBas = dataPasBas;
				this.stromType = "未开始";
			});
		},
		methods: {
			liClick(index) {
				let _this = this;
				//				this.dateLength = this.dateLength + 1;
				if(this.dataPas[index].dataType) {
					this.dataPas[index].paseIne = 'radio';
					this.dataPas[index].dataType = false;
					this.dataPas[index].index = index;

					var linDataPas = this.dataPas;
					linDataPas = linDataPas.filter(t => t.paseIne != 'radio' && t.paseIne != 'cha');
					var x = parseInt(Math.random() * linDataPas.length - 1);
					console.log(linDataPas[x]);
					//				console.log(linDataPas);
					for(var i = 0; i < this.dataPas.length; i++) {
						console.log(linDataPas[x].index);
						console.log(this.dataPas[i].index);
						console.log("--------------------")
						if(linDataPas[x].index == this.dataPas[i].index) {
							this.dataPas[i].paseIne = 'cha';
							this.dataPas[i].dataType = false
						}
					}
				}
				//				var  x=parseInt(Math.random()*this.buttonObj.length-1);
				//				var corb=this.buttonObj[x];
				//				console.log(this.buttonObj);
				if((this.dataPas[0].paseIne == 'radio' && this.dataPas[1].paseIne == 'radio' && this.dataPas[2].paseIne == 'radio') || //第一排横  ——————
					(this.dataPas[0].paseIne == 'radio' && this.dataPas[3].paseIne == 'radio' && this.dataPas[6].paseIne == 'radio') || //第一列竖|
					(this.dataPas[0].paseIne == 'radio' && this.dataPas[4].paseIne == 'radio' && this.dataPas[8].paseIne == 'radio') || //第一个开始到最后一斜\
					(this.dataPas[1].paseIne == 'radio' && this.dataPas[4].paseIne == 'radio' && this.dataPas[7].paseIne == 'radio') || //第二列竖|
					(this.dataPas[2].paseIne == 'radio' && this.dataPas[5].paseIne == 'radio' && this.dataPas[8].paseIne == 'radio') || //第三列 竖|
					(this.dataPas[2].paseIne == 'radio' && this.dataPas[4].paseIne == 'radio' && this.dataPas[6].paseIne == 'radio') || //   /斜
					(this.dataPas[3].paseIne == 'radio' && this.dataPas[4].paseIne == 'radio' && this.dataPas[5].paseIne == 'radio') || //第二排横——
					(this.dataPas[6].paseIne == 'radio' && this.dataPas[7].paseIne == 'radio' && this.dataPas[8].paseIne == 'radio') //第三行——————
				) {
					this.textList = "实心胜";
					this.stromType = "游戏结束";
//					setTimeout(function() {
//						_this.stromType = "未开始";
//						_this.clearLine();
//						_this.textList = "";
//					}, 1500);
					for(var i = 0; i < this.dataPas.length; i++) {
						this.dataPas[i].dataType = false;
					}
				} else if((this.dataPas[0].paseIne == 'cha' && this.dataPas[1].paseIne == 'cha' && this.dataPas[2].paseIne == 'cha') ||
					(this.dataPas[0].paseIne == 'cha' && this.dataPas[3].paseIne == 'cha' && this.dataPas[6].paseIne == 'cha') ||
					(this.dataPas[0].paseIne == 'cha' && this.dataPas[4].paseIne == 'cha' && this.dataPas[8].paseIne == 'cha') ||
					(this.dataPas[1].paseIne == 'cha' && this.dataPas[4].paseIne == 'cha' && this.dataPas[7].paseIne == 'cha') ||
					(this.dataPas[2].paseIne == 'cha' && this.dataPas[5].paseIne == 'cha' && this.dataPas[8].paseIne == 'cha') ||
					(this.dataPas[2].paseIne == 'cha' && this.dataPas[4].paseIne == 'cha' && this.dataPas[6].paseIne == 'cha') ||
					(this.dataPas[3].paseIne == 'cha' && this.dataPas[4].paseIne == 'cha' && this.dataPas[5].paseIne == 'cha') || //第二排横——
					(this.dataPas[6].paseIne == 'cha' && this.dataPas[7].paseIne == 'cha' && this.dataPas[8].paseIne == 'cha') //第三行——————
				) {
					this.textList = "空心胜";
					this.stromType = "游戏结束";
//					setTimeout(function() {
//						_this.stromType = "未开始";
//						_this.clearLine();
//						_this.textList = "";
//					}, 1500);
					for(var i = 0; i < this.dataPas.length; i++) {
						this.dataPas[i].dataType = false;
					}
				}
			},
			//清空棋盘
			clearLine() {
				this.dataPas = [{
					paseIne: '',
					dataType: false,
					index: '0'
				}, {
					paseIne: '',
					dataType: false,
					index: '1'
				}, {
					paseIne: '',
					dataType: false,
					index: '2'
				}, {
					paseIne: '',
					dataType: false,
					index: '3'
				}, {
					paseIne: '',
					dataType: false,
					index: '4'
				}, {
					paseIne: '',
					dataType: false,
					index: '5'
				}, {
					paseIne: '',
					dataType: false,
					index: '6'
				}, {
					paseIne: '',
					dataType: false,
					index: '7'
				}, {
					paseIne: '',
					dataType: false,
					index: '8'
				}]
			},
			//开始游戏
			start() {
				this.clearLine();
				for(var i = 0; i < this.dataPas.length; i++) {
					this.dataPas[i].dataType = true;
				}
				this.stromType = "进行中";
				this.textList = "";
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.bodyUl {
		width: 800px;
		height: 800px;
		/*border: 1px  solid black;*/
		padding: 0;
		margin: auto;
	}
	
	.bodyUl li {
		width: 33.33%;
		height: 33.33%;
		list-style: none;
		float: left;
		border: 1px solid;
		box-sizing: border-box;
	}
	
	.radio {
		background: #000000;
		width: 100%;
		height: 100%;
		border-radius: 50%;
	}
	
	.cha {
		width: 99%;
		height: 99%;
		border-radius: 50%;
		border: 1px solid #ffc107;
	}
	
	.rightTextBut {
		position: absolute;
		top: 0;
		height: 500px;
		width: 500px;
		bottom: 0;
		margin: auto;
	}
</style>