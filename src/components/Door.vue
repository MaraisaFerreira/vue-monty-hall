<template>
	<div class="door-area">
		<div class="door-frame">
			<Gift v-if="open && hasGift" />
			<Error v-if="open && !hasGift" />
		</div>
		<div class="door" @click="selected = !selected" :class="{ selected, open }">
			<div class="img-box">
				<img src="../assets/imgs/door.jpg" />
			</div>
			<div class="number">{{ number }}</div>
		</div>
	</div>
</template>

<script>
import Gift from './Gift';
import Error from './Error';

export default {
	name: 'Door',
	components: { Gift, Error },
	props: {
		number: {},
		hasGift: { type: Boolean },
	},

	data() {
		return {
			open: false,
			selected: false,
		};
	},
};
</script>

<style>
:root {
	--border-frame: solid 11px #c7660ce0;
}

.door-area {
	position: relative;
	width: 200px;
	height: 310px;
	margin-bottom: 20px;
	display: flex;
	justify-content: center;
	font-size: 1.3rem;
}

.door-frame {
	position: absolute;
	width: 100%;
	height: 100%;
	display: flex;
	justify-content: center;
	align-items: flex-end;

	border-top: var(--border-frame);
	border-right: var(--border-frame);
	border-left: var(--border-frame);
	background: black;
}

.door {
	position: absolute;
	width: 100%;
	height: 100%;

	display: flex;
	flex-direction: column;
	align-items: center;
}

.img-box {
	position: absolute;
	width: 100%;
	height: 100%;
}

.img-box img {
	width: 100%;
	height: 100%;
}

.door .number {
	position: absolute;
	z-index: 10;
	margin-top: 69px;
	width: 30px;
	border: 1px solid black;
	background: #0009;
	border-radius: 5px;
	display: flex;
	align-items: center;
	justify-content: center;
}

.door.selected {
	box-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #fff, 0 0 20px #ccff00,
		0 0 20px #ccff00, 0 0 20px #ccff00, 0 0 25px #ccff00, 0 0 20px #ccff00;
}

.door.open {
	display: none;
}

.door.open .img-box {
	display: none;
}

.door.open .number {
	display: none;
}
</style>
