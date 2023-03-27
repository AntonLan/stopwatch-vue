<template>
	<div class='wrapper'>
		<div class='number-wrapper'>
			<p
				v-if='timer.hour > 0'
				:class="timer.isActive ? 'timer-active' : ''"
			>{{ timer.hour }}:</p>
			<p v-if='timer.minute > 0'
				 :class="timer.isActive ? 'timer-active' : ''"
			>{{ timer.minute }}:</p>
			<p
				:class="timer.isActive ? 'timer-active' : ''"
			>{{ timer.second }}</p>
		</div>
		<hr
			:class="timer.isActive ? 'divider-active' : 'divider'">
		<div class='btn-wrapper'>
			<button
				v-if='!timer.isActive'
				@click="$emit('start', timer)">
				<div class='start-btn'></div>
			</button>
			<button
				v-if='timer.isActive'
				@click="$emit('pause', timer)">
				<div class='pause-btn'>
					<div></div>
				</div>
			</button>
			<button
				@click="$emit('reset', timer)">
				<div
					:class="timer.isActive ? 'square-active' : 'square'">
				</div>
			</button>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		timer: {
			type: Object,
			required: true
		}
	}
}
</script>

<style lang='scss' scoped>

.wrapper {
	width: 225px;
	height: 120px;
	background: #696969;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;

	.number-wrapper {
		display: flex;
		text-align: center;

		p {
			background: #696969;
			padding-bottom: 15px;
			font-weight: 400;
			font-size: 22px;
			color: #9E9E9EFF;
		}

		.timer-active {
			background: #696969;
			padding-bottom: 15px;
			font-weight: 400;
			font-size: 22px;
			color: white;
		}
	}


	.divider {
		border-top: 1px solid #9E9E9EFF;
		border-bottom: #9E9E9EFF;
		width: 225px;
	}

	.divider-active {
		border-top: 1px solid white;
		border-bottom: white;
		width: 225px;
	}

	.btn-wrapper {
		display: flex;
		background: #696969;
		gap: 52px;
		padding-top: 20px;

		button {
			background: none;
			border: none;
		}

		.square {
			cursor: pointer;
			width: 20px;
			height: 20px;
			left: 270px;
			top: 317px;
			background: #9E9E9E;
		}

		.square-active {
			cursor: pointer;
			margin-left: 3px;
			width: 20px;
			height: 20px;
			left: 270px;
			top: 317px;
			background: white;
		}

		.start-btn {
			cursor: pointer;
			width: 0;
			height: 0;
			border-top: 10px solid #696969;
			border-left: 17px solid #9E9E9EFF;
			border-bottom: 10px solid #696969;
		}


		.pause-btn {
			cursor: pointer;
			margin-right: 10px;
			width: 3px;
			height: 20px;
			background: white;

			div {
				margin-left: 6px;
				position: absolute;
				width: 3px;
				height: 20px;
				background: white;
			}
		}

	}

}

</style>