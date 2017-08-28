<template>
<span>
	<!-- Day input -->
	<input type="number" min="1" class="day-input"
		v-model="input.day" :max="numberOfDaysInMonth" >

	<!-- Month input -->
	<select v-model="input.month">
		<option v-for="(month,key) in config.months"
			:value="key">{{month}}</option>
	</select>
	
	<!-- Year input -->
	<input v-model="input.year" 
		class="year-input" type="number">
</span>
</template>






<style scoped>
.day-input{
	width:50px;
}
.year-input{
	width:100px;
}
</style>








<script>
import config from './config.js'

export default {
	


	data(){return{
		config,
		input:{
			month:0,
			year:config.year.default,
			day:1
		}
	}},

	computed:{
		numberOfDaysInMonth(){
			var month = this.input.month
			if(month == 1)
			{
				var year = this.input.year
				//February has 29 days if it a leap year
				if(year % 4==0 ||year % 400==0) 
					return 29

				return 28
			}

			if( month==3 ||month==5 ||month==8 ||month==10)
				return 30
			return 31
		},
		dateString(){
			return this.input.year+'-'+(this.input.month +1 )+'-'+this.input.day
		},
		date(){
			return new Date(this.dateString);
		}
	},




}
</script>

