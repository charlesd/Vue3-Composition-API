<template>
  <div class="hello">
	<table style="text-align: left">
	  <thead>
	    <tr>
		  <th>Name</th>
		  <th>Population</th>
	    </tr>
	  </thead>
	  <tbody>
	    <tr v-for="({name, population}, index) in countries" :key="index">
		  <td>{{name}}</td>
		  <td>{{population}}</td>
	    </tr>
	  </tbody>
	</table>
	<div style="text-align: left;">{{counter}} countries listed.</div>
  </div>
</template>

<script>
import { ref, watch, onMounted } from 'vue'
import axios from 'axios'

export default {
  name: "HelloWorld",
  props: {
  },
  setup(){
	const countries = ref([])
	const counter = ref(0)
	watch(countries, (newValue, oldValue) => {
	//	console.log('countries: ' + countries.value)
		counter.value = newValue.length
	})
	onMounted(() => {
		axios(`https://restcountries.eu/rest/v2/regionalbloc/nafta`)
			.then(response => countries.value = response.data)
	})
	return {
		countries,
		counter
	}
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
