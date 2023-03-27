<template>
	<div class='container'>
		<TimerItem
			:key='timer.id'
			v-for='timer in timers'
			:timer='timer'
			@start='start'
			@pause='pause'
			@reset='reset'
		/>
		<button class='btn' @click='createTimer'>
			<div class='plus-btn'>
				<div></div>
			</div>
		</button>
	</div>
</template>

<script>
import TimerItem from '@/components/TimerItem.vue'

export default {
	components: { TimerItem },
	data() {
		return {
			timers: [
				{
					id: Date.now(),
					isActive: false,
					hour: 0,
					minute: 0,
					second: 0,
					started: undefined
				}
			]
		}
	},
	methods: {
		start(time) {
			this.timers.map(e => {
				if (time.id === e.id) {
					e.isActive = true
					this.checkStatus(e)
				}
			})
		},
		pause(time) {
			this.timers.map(e => {
				if (time.id === e.id) {
					e.isActive = false
					this.checkStatus(e)
				}
			})
		},
		reset(time) {
			this.timers.map(e => {
				if (time.id === e.id) {
					clearTimeout(e.started)
					e.isActive = false
					e.hour = 0
					e.minute = 0
					e.second = 0
					e.started = undefined
				}
			})
		},
		checkStatus(value) {
			if (value.isActive) {
				value.started = setTimeout(() => {
					value.second++
					if (value.second === 60) {
						value.second = 0
						value.minute++
					}
					if (value.minute === 60) {
						value.second = 0
						value.minute = 0
						value.hour++
					}
					this.start(value)
				}, 1000)
			} else {
				clearTimeout(value.started)
			}
		},
		createTimer() {
			let newTimer = {
				id: Date.now(),
				isActive: false,
				hour: 0,
				minute: 0,
				second: 0,
				started: undefined
			}
			this.timers.push(newTimer)
		}
	}
}
</script>

<style lang='scss' scoped>
.container {
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translateX(-50%) translateY(-50%);
	margin: 72px 0 72px 0;
	row-gap: 50px;
	column-gap: 45px;

	.btn {
		width: 225px;
		height: 120px;
		cursor: pointer;
		border: none;
		background: #696969;

		.plus-btn {
			margin: auto;
			width: 3px;
			height: 20px;
			background: #9E9E9E;

			div {
				position: absolute;
				width: 3px;
				height: 20px;
				background: #9E9E9E;
				transform: rotate(-90deg)
			}
		}
	}
}


</style>