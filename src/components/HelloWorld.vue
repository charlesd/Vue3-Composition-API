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
	<div style="text-align: left;">{{link}}</div>
  </div>
</template>

<script>
import { ref, watch, computed, onMounted, toRefs } from 'vue'
import axios from 'axios'

export default {
  name: "HelloWorld",
  props: {
    url: {
      type: String,
      required: true
    }
  },
  setup(props){
	const { url } = toRefs(props)
	const countries = ref([])
	const counter = ref(0)
	const link = computed(() => '*** '+url.value+' ***')

	watch(countries, (newValue, oldValue) => {
	//	console.log('countries: ' + countries.value)
		counter.value = newValue.length
	})
	onMounted(() => {
		axios(url.value)
			.then(response => countries.value = response.data)
	})
	return {
		countries,
		counter,
		link
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
