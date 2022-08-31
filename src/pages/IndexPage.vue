<template>
  <div class="row q-gutter-x-md q-ma-md">
		<div class="col">
			<div class="colunn q-gutter-md">
				<div class="col">
					<q-input label="Clau" v-model="clau" autofocus></q-input>
				</div>
				<div class="col">
					<q-input label="Categories" v-model="categories"></q-input>
				</div>
				<div class="col">
					<q-input label="Titol" v-model="titol"></q-input>
				</div>
				<div class="col">
					<q-input
						type="textarea"
						v-model="text"
						clearable
						autogrow
						filled
					/>
				</div>
			</div>
		</div>

		<div class="col">
			<div class="column q-gutter-md">
				<div class="col">
					<q-btn label="Copiar" dense @click="copiar" />
				</div>
				<div class="col bg-yellow-3">
					<pre>{{ objResultat }}</pre>
				</div>
			</div>
			
		</div>
  </div>
</template>

<script setup>
	import { ref, computed } from 'vue'
	import { copyToClipboard } from 'quasar'

	let clau = ref('')
	let titol = ref('')
	let categories = ref('')
	let text = ref('')

	let objResultat = computed( () => {
		let arr = ""
		if (text.value !== null) {
			arr = []
			const arrText = text.value.split('\n')

			arrText.forEach( (linia) => {
				arr.push( linia )
			})
		}

		let obj = {}
		obj[clau.value] = {}
		obj[clau.value].titol = titol.value
		obj[clau.value].categories = categories.value.split(",").map( cat => (cat.trim()))
		obj[clau.value].arrText = arr

		
		return obj
	})




	const copiar =() => {

		let objString = document.getElementsByTagName('pre')[0].innerHTML.trim()
		
		objString = objString.substring(1, objString.length - 2) + ","
		copyToClipboard(objString)
		.then((arr) => {
			
		})
		.catch(() => {
			// fail
		})
	}


// import { defineComponent } from 'vue'

// export default defineComponent({
//   name: 'IndexPage'
// })
</script>
