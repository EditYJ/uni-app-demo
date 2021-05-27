<template>
	<view class="todo-list">
		<text v-if="restTask == 0">恭喜！今日任务已全部完成！</text>
		<text v-else>今日剩余任务量: {{restTask}}</text>
		<view class="add-task-wrapper">
			<uni-forms :value="formData" ref="taskForm">
				<uni-forms-item label="任务名称" name="task">
					<uni-easyinput type="text" v-model="formData.task" placeholder="请输入任务名称"></uni-easyinput>
				</uni-forms-item>
			</uni-forms>
			<button class="btn" type="primary" @click="addTask">添加任务</button>
		</view>
		<view class="checbox-wrapper">
			<uni-data-checkbox mode="list" v-model="finishTasks" multiple="true" :localdata="taskList"
				@change="checkBoxChange">
			</uni-data-checkbox>
		</view>
		<view class="btn-group">
			<button class="btn" type="primary" @click="finishAll">完成全部</button>
			<button class="btn" type="primary" @click="clearAll">清除全部</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				formData: {
					task: ''
				},
				finishTasks: [],
				taskList: [{
					value: 0,
					text: "早上打篮球"
				}, {
					value: 1,
					text: "下午踢足球"
				}, {
					value: 2,
					text: "晚上去游泳"
				}]
			};
		},
		computed: {
			restTask() {
				return this.taskList.length - this.finishTasks.length || 0
			}
		},
		methods: {
			checkBoxChange(e) {
				console.log('e: ', e)
			},
			addTask() {
				const taskItem = {
					value: this.taskList.length,
					text: this.formData.task
				}
				this.taskList.push(taskItem)
			},
			finishAll() {
				this.finishTasks = this.taskList.map(item => item.value)
			},
			clearAll() {
				this.finishTasks = []
			}
		}
	}
</script>

<style lang="scss">
	.todo-list {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		.add-task-wrapper {
			margin-top: 28rpx;

			.uni-forms-item__inner {
				padding-bottom: 0rpx;
			}
		}

		.checbox-wrapper {
			margin-top: 28rpx;
			width: 500rpx;
		}

		.btn-group {
			display: flex;
		}

		.btn {
			width: auto;
			height: 74rpx;
			display: flex;
			align-items: center;
			justify-content: center;
			font-size: 30rpx;
			background-color: #007aff;
			margin: 16rpx;
		}
	}
</style>
