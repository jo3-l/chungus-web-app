<template>
	<div id="app">
		<h1>Make a Chungus</h1>
		<strong>Chungus name: </strong> <input v-model="name" placeholder="enter le name" />
		<p>
			Your chungus name is: <strong>{{ name }}</strong>
		</p>

		<strong>Chungus size: </strong>
		<select v-model="selected">
			<option v-for="size in sizes" :key="size">
				{{ size }}
			</option>
		</select>

		<p>
			Your preferred chungus size is: <strong>{{ selected }}</strong>
		</p>
		<img :src="chungusImageURL" height="300" />

		<p>
			Your chungus needs a nickname! Here is our suggestion: <strong>{{ chungusNickname }}</strong>
		</p>
	</div>
</template>

<script>
const descriptors = [
	'smelly',
	'strong',
	'buff',
	'chunky',
	'not real',
	'real',
	'substantial',
	'colossal',
	'inflated',
	'big',
];

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

		chungusNickname() {
			const descriptor = descriptors[Math.floor(Math.random() * descriptors.length)];
			return `${this.selected}-sized ${descriptor} chungus`;
		},
	},
};
</script>

<style>
body {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: left;
	color: #dddddd;
	margin-top: 60px;
	margin-left: 60px;
	background-color: #141414;
}
</style>
