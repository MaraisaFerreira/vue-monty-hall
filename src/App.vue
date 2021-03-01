<template>
	<div id="app">
		<h1>Desafio: Monty Hall</h1>
		<div>
			<!-- inicial -->
			<h2 v-if="!selected">Em qual porta está o presente?</h2>
			<h5 v-if="!selected">(Selecione uma porta)</h5>

			<!-- primeira msg -->
			<h2 v-if="selected && chances == 1">
				Tem Certeza? Não quer trocar de porta?
			</h2>
			<h5 v-if="selected && chances == 1">
				Vou te ajudar, nas portas {{ numberMsg }}, o presente NÃO está!
			</h5>

			<!-- segunda msg -->
			<h2 v-if="selected && chances == 2">
				Última chance de trocar!
			</h2>
			<h5 v-if="selected && chances == 2">
				Nas portas {{ numberMsg }}, o presente NÃO está!
			</h5>

			<!-- fim de jogo -->
			<div v-if="chances == 3">
				<h1 v-if="win">
					Ganhou! Parabéns!
				</h1>
				<h1 v-if="!win">Perdeu!</h1>
			</div>
		</div>
		<div class="doors">
			<div
				v-for="i in doorsAmount"
				:key="i"
				@click="setSelected(i)"
				:id="'door' + i"
			>
				<Door
					:class="{
						doorSelected: i == selected,
						open: openedDoors.includes(i),
					}"
					:hasGift="i === doorRewarded"
					:number="i"
					:open="openedDoors.includes(i)"
				/>
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
			doorsAmount: null,
			doorRewarded: null,
			selected: false,
			openedDoors: [],
			toOpen: [],
			chances: 0,
			win: false,
		};
	},
	methods: {
		//gera a qtd de portas do jogo
		getDoorsAmount() {
			return Math.floor(Math.random() * 5 + 5); //max 10 portas
		},

		//gera qual porta tá com o presente
		getDoorRewarded() {
			return Math.floor(Math.random() * (this.doorsAmount - 1) + 1); //de 1 a qtd portas
		},

		//selec/dessel as portas
		setSelected(idx) {
			if (this.openedDoors.includes(idx)) {
				return; //já aberta
			}

			if (this.selected != null) {
				if (this.selected != this.doorRewarded) {
					this.toOpen.push(this.selected); //add a porta antiga
				}
				this.toOpen = this.toOpen.filter((item) => {
					return item != idx && parseInt(item);
				}); //remove a nv
			}

			this.selected = idx; //altera a seleção
			console.log('ToOpen', this.toOpen);
			this.openDoors();
		},

		//abre as portas não premiadas ou selecionada
		openDoors() {
			console.log('OPEN');
			if (this.chances == 0) {
				console.log('Chances == 0');
				const times = Math.ceil(this.toOpen.length / 2);
				for (let i = 0; i < times; i++) {
					const n = Math.floor(Math.random() * this.toOpen.length);
					this.openedDoors.push(this.toOpen[n]);
					this.toOpen.splice(n, 1);
				}
				this.openedDoors.sort(this.orderByNumber);
				console.log('Fechadas', this.toOpen, '/ Abertas', this.openedDoors);
				this.chances++;
			} else if (this.chances == 1) {
				console.log('Chances == 1');
				let n = this.toOpen.length;
				if (this.selected == this.doorRewarded) {
					n--;
					console.log('-n');
				}

				let temp = [];
				for (let i = 0; i < n; i++) {
					console.log('> ', this.toOpen[i], i);
					this.openedDoors.push(this.toOpen[i]);
					temp.push(this.toOpen[i]);
				}

				this.toOpen = this.toOpen.filter((item) => !temp.includes(item));
				this.openedDoors.sort(this.orderByNumber);
				console.log('Fechadas', this.toOpen, '/ Abertas', this.openedDoors);
				this.chances++;
			} else {
				console.log('Finalizar jogo');
				console.log('Fechadas', this.toOpen, '/ Abertas', this.openedDoors);
				for (let i = 0; i < this.toOpen.length; i++) {
					this.openedDoors.push(this.toOpen[i]);
					this.toOpen.splice(i, 1);
				}

				this.openedDoors.push(this.doorRewarded);

				if (!this.openedDoors.includes(this.selected)) {
					this.openedDoors.push(this.selected);
				}
				this.chances++;

				if (this.selected == this.doorRewarded) {
					this.win = true;
				}
			}
		},

		/* funções auxiliares */

		orderByNumber(a, b) {
			return a - b;
		},

		getStr() {
			let str = '';
			for (let i = 0; i < this.openedDoors.length; i++) {
				if (i < this.openedDoors.length - 2) {
					str += `${this.openedDoors[i]}, `;
				} else if (i == this.openedDoors.length - 2) {
					str += `${this.openedDoors[i]} e `;
				} else {
					str += `${this.openedDoors[i]}`;
				}
			}
			return str;
		},
	},

	computed: {
		numberMsg() {
			return this.getStr();
		},
	},

	mounted() {
		this.doorsAmount = this.getDoorsAmount();
		this.doorRewarded = this.getDoorRewarded();

		let n = 1;
		while (n <= this.doorsAmount) {
			if (n != this.doorRewarded) {
				this.toOpen.push(n);
			}
			n++;
		}

		console.log(
			'N portas =',
			this.doorsAmount,
			'/ Premiada =',
			this.doorRewarded,
			'/ Pd abrir',
			this.toOpen
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
	margin-bottom: 20px;
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
