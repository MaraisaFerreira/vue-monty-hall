<template>
	<div id="app">
		<h1>Monty Hall</h1>
		<div v-if="!started">
			<h2 id="info-txt">Em qual porta está o presente?</h2>
			<h5 id="help-txt">(Selecione uma porta)</h5>
		</div>
		<div class="doors">
			<div v-for="i in doorsAmount" :key="i">
				<Door :hasGift="i === doorRewarded" :number="i" />
			</div>
		</div>
	</div>
</template>

<script>
import Door from './components/Door';

export default {
	name: 'App',
	components: { Door },
	data() {
		return {
			started: false,
			doorsAmount: null,
			selectedDoor: null,
			doorRewarded: null,
		};
	},

	methods: {
		getDoorsAmount() {
			return Math.floor(Math.random() * 10 + 5);
		},

		getDoorRewarded() {
			return Math.floor(Math.random() * this.doorsAmount);
		},
	},

	mounted() {
		this.doorsAmount = this.getDoorsAmount();
		this.doorRewarded = this.getDoorRewarded();
		console.log(
			'portas =',
			this.doorsAmount,
			'/ premiada =',
			this.doorRewarded
		);
	},
};
</script>

<style>
:root {
	/* Sombras */
	--shadow-txt: 1px 1px 3px #0006;
	--shadow-h1: 2px 2px 3px #0009;

	/* Gradientes */
	--bg: linear-gradient(to right, #080e60 0%, #121fcf 39%, #ca63ce 100%);
}

* {
	box-sizing: border-box;
	font-family: 'Montserrat', sans-serif;
	padding: 0;
	margin: 0;
}

body {
	color: white;
	background: #121fcf;
	background: var(--bg);
}

#app {
	display: flex;
	flex-direction: column;
	align-items: center;
}

#app h1 {
	text-shadow: var(--shadow-h1);
	background: #0008;
	padding: 15px;
	margin-top: 10px;
	border: 1px solid black;
	text-align: center;
}

#app h2 {
	margin-top: 10px;
	text-align: center;
	text-shadow: var(--shadow-txt);
}

#app h5 {
	margin-top: 10px;
	margin-bottom: 20px;
	text-align: center;
	text-shadow: var(--shadow-txt);
}

.doors {
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	flex-wrap: wrap;
}
</style>
