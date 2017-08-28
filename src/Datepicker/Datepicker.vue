<template>
<span>
	<!-- Day input -->
	<input type="number" min="1" class="day-input"
		:value="input.day" :max="numberOfDaysInMonth" 
		@input="onDayInput">

	<!-- Month input -->
	<select  :value="input.month" 
		@input="onMonthInput">
		
		<option v-for="(month,key) in config.months"
			:value="key">{{month}}</option>
	</select>
	
	<!-- Year input -->
	<input class="year-input" type="number"
		 :value="input.year" 
		@input="onYearInput">
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
	props:{
		day:{
			default:(new Date()).getDate()
		},
		month:{
			default:(new Date()).getMonth()-1
		},
		year:{
			default:(new Date()).getFullYear()
		}
	},

	data(){return{
		config,
		input:{
			month:this.month,
			year:this.year,
			day:this.day
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
		}
	},
	methods:{
		onDayInput(e){
			this.input.day  = parseInt(e.target.value)
			this.$emit('input',this.dateString)
		},
		onMonthInput(e){
			this.input.month  = parseInt(e.target.value)
			this.$emit('input',this.dateString)
		},
		onYearInput(e){
			this.input.year  = parseInt(e.target.value)
			this.$emit('input',this.dateString)
		}

	}



}
</script>

