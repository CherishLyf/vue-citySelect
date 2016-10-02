<template lang="html">
  <div>
    <select v-model="province">
      <option value="">请选择</option>
      <option v-for="item in provinces" value="{{item}}">{{ item }}</option>
    </select>
    <select v-model="city">
      <option value="">请选择</option>
      <option v-for="item in citys" value="{{item}}">{{ item }}</option>
    </select>
    <select v-model="county">
      <option value="">请选择</option>
      <option v-for="item in countys" value="{{item}}">{{ item }}</option>
    </select>
  </div>
</template>

<script>
export default {
  props:{
		province:{
			type:String,
			default:''
		},
		city:{
			type:String,
			default:''
		},
		county:{
			type:String,
			default:''
		}
	},
	data:function(){
		return {
			addressData:null
		}
	},
	init:function(){
		var that=this
		setTimeout(function(){
			that.addressData={
				'河南':{
					'新乡':{
						"牧野区":{},
						"红旗区":{}
					},
					'郑州':{
						'金水区':{},
						'高新区':{}
					}
				},
				'浙江':{
					'杭州':{
						'萧山区':{}
					}
				}
			}
		},1000)
	},
	watch:{
		province:function(val,oldval){
			if(val!==oldval){
				this.city=''
			}
		},
		city:function(val,oldval){
			if(val!==oldval){
				this.county=''
			}
		}
	},
	computed:{
		provinces:function(){
			if(!this.addressData)return

			var c=[]
			for(var key in this.addressData){
				c.push(key)
			}

			return c
		},
		citys:function(){
			if(!this.addressData
				|| !this.province)
				return

			var c=[]
			for(var key in this.addressData[this.province]){
				c.push(key)
			}

			return c
		},
		countys:function(){
			if(!this.addressData
				||!this.city)
				return

			var c=[]
			for(var key in this.addressData[this.province][this.city]){
				c.push(key)
			}

			return c
		}
	}
};
</script>

<style lang="css">
</style>
