<template>
	<div class="door-area">
		<div class="door-frame">
			<Gift v-if="open && hasGift" />
			<Error v-if="open && !hasGift" />
		</div>
		<div :class="{ door: !open, opened: open }">
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
		open: { type: Boolean },
	},
};
</script>

<style>
:root {
	/* Bordas */
	--border-frame: solid 11px #8d4705e0;
	/* Medidas */
	--door-width: 200px;
	--door-height: 310px;
	--door-margin: 10px;
	/* Cores */
	--bg-opened-door: #000;
	--bg-number: #0009;
	/* Sombras */
	--selected-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #fff,
		0 0 20px #ccff0095, 0 0 20px #ccff0095, 0 0 20px #ccff0095,
		0 0 25px #ccff0095, 0 0 20px #ccff0095;
}

.door-area {
	position: relative;
	width: var(--door-width);
	height: var(--door-height);
	margin-bottom: 20px;
	display: flex;
	justify-content: center;
	font-size: 1.3rem;
	margin-right: var(--door-margin);
	margin-left: var(--door-margin);
	overflow: hidden;
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
	border-bottom: 5px solid black;
	background: var(--bg-opened-door);
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
	background: var(--bg-number);
	border-radius: 5px;
	display: flex;
	align-items: center;
	justify-content: center;
}

.opened img {
	display: none;
}

.doorSelected {
	box-shadow: var(--selected-shadow);
}
</style>
