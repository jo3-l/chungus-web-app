<template>
	<div id="app">
		<h1>make a chungus</h1>
		Chungus name: <input v-model="name" />
		<p>Your chungus name is: {{ name }}</p>

		<select v-model="selected">
			<option v-for="size in sizes" :key="size">
				{{ size }}
			</option>
		</select>

		<p>
			Your preferred chungus size is: <strong>{{ selected }}</strong>
		</p>
		<img :src="chungusImageURL" height="300" />
	</div>
</template>

<script>
export default {
	data() {
		return {
			name: '',
			selected: 'big',
			sizes: ['big', 'medium', 'small'],
		};
	},

	mounted() {
		this.name = localStorage.getItem('name');
	},

	watch: {
		name(newName) {
			localStorage.setItem('name', newName);
		},
	},

	computed: {
		chungusImageURL() {
			const images = require.context('./assets', false, /\.png$/);
			return images(`./${this.selected}chungus.png`);
		},
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
