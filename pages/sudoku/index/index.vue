<template>
	<view class="content">
		<view class="gongge" v-for="(item,index) in array" :key="index">
			<view class="grid" v-for="(items,index1) in item.arr" :key="index1">
				{{items}}
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			array: [],
			again: false
		}
	},
	watch: {
		again() {
			console.log(this.again,'again')
			// this.getOrigin()
		},
	},
	methods: {
		getRandomInt() {
			return Math.floor(Math.random() * (10 - 1)) + 1; //不含最大值，含最小值
		},
		getNum(index) {
			this.again = false
			var already = false
			for(var i=0; i<this.array[index].arr.length;){
				for(var j=0; j<20; j++){
					var num = this.getRandomInt()
					if(index == 0 || index == 4 || index == 8){
						if(this.array[index].arr.indexOf(num) == -1){
							this.array[index].arr[i] = num
							i++
							break;
						}
					}else{			
						var leftRow = '',
							 leftCol = [],
							 bottomRow = '',
							 bottomCol = [];
						leftRow = index < 3 ? 0 : index < 6 ? 4 : 8
						leftCol = i < 3 ? [0,1,2] : i < 6 ? [3,4,5] : [6,7,8]
						bottomRow = index == 1 || index == 7 ? 4 : index == 2 || index == 5 ? 8 : 1
						bottomCol = i == 0 || i == 3 || i == 6 ? [0,3,6] : i == 1 || i == 4 || i == 7 ? [1,4,7] : [2,5,8]
						if(num != this.array[leftRow].arr[leftCol[0]] && num != this.array[leftRow].arr[leftCol[1]] && num != this.array[leftRow].arr[leftCol[2]] && 
							num != this.array[bottomRow].arr[bottomCol[0]] && num != this.array[bottomRow].arr[bottomCol[1]] && num != this.array[bottomRow].arr[bottomCol[2]]){
							// this.array[index].arr[i] = num
							if(this.array[index].arr.indexOf(num) == -1){
								this.array[index].arr[i] = num
								console.log(num,'i')
								already = true
								i++
								break;
							}
							if(this.array[index].arr.indexOf(0) != -1){
								this.again = true
							}
					
						}
					}				
				}
				if(already){
					continue;
				}
			}
			// this.array[1].arr[0]   //row: 1    col: 0  
			// this.array[0].arr[0]   //leftRow、leftCol、bottomRow、bottomCol
			// this.array[0].arr[1]
			// this.array[0].arr[2]
			// this.array[4].arr[0]
			// this.array[4].arr[3]
			// this.array[4].arr[6]
			
			// this.array[1].arr[1]   //row: 1    col: 0
			// this.array[0].arr[0]   //num、num1
			// this.array[0].arr[1]
			// this.array[0].arr[2]
			// this.array[4].arr[1]
			// this.array[4].arr[4]
			// this.array[4].arr[7]
			
			// this.array[1].arr[1]
			// this.array[1].arr[2]
		},
		getOrigin() {
			for(var i=1; i<10; i++){
				var obj = {
					arr: []
				}
				for(var j=1; j<10; j++){
					obj.arr.push(0)
				}
				this.array.push(obj)
			}
			this.getNum(0)
			// this.getNum(4)
			// this.getNum(8)
			this.getNum(1)
			this.getNum(2)
		},
		getFull(row,col){
			
		}
	},
	onLoad() {
		this.getOrigin()
	}
}
</script>

<style lang="scss" scoped>
.content{
	padding: 30upx;
}
.gongge{
	display: inline-block;
	width: 33.3%;
}
.grid{
	display: inline-block;
	width: 33.3%;
	height: 60upx;
	line-height: 60upx;
	text-align: center;
}
</style>
