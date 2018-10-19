<template>
  <div class="todo-main">
    <div class="todo-title">
      Todo
    </div>
    <div class="form-item">
      <span class="form-item-left">任务</span>
      <span class="form-item-right">
        <input type="text" placeholder="请输入任务" class="form-item-right-input" v-model="curTask">
        <span class="form-item-right-add" @click="addTask">添加</span>
      </span>
    </div>
    <div class="todo-list">
      <div class="todo-list-item" v-for="(item, index) in todoLists" :key="index" v-show="item.isShow"> 
        <span class="iconfont icon-wode todo-icon-body"></span>
        <span class="todo-list-item-task" :class="{'task-finish': item.isFinished}">{{item.taskName}}</span>
        <span class="iconfont icon-yigouxuan todo-icon-check" :class="{'isFinished': item.isFinished}" @click="finishClick(index)"></span>
        <span class="iconfont icon-shanchu todo-icon-delete" @click="deleteClick(index)"></span>
      </div>
    </div>
    <mp-toast :type="toastList.toastType" v-model="toastList.isEmty" :content="toastList.toastContent" :duration="toastList.toastDuration"></mp-toast>
  </div>
</template>
<script>
import mpToast from 'mpvue-weui/src/toast'
export default {
  components: {
    mpToast
  },
  data () {
    return {
      curTask: '',
      todoLists: [],
      toastList: {
        isEmty: false,
        toastType: 'warn',
        toastContent: '请输入任务',
        toastDuration: 2000
      }
    }
  },
  methods: {
    addTask () {
      if (this.curTask === '') {
        this.toastList.isEmty = true
        return false
      } else {
        this.todoLists.push({
          taskName: this.curTask,
          isFinished: false,
          isShow: true
        })
        this.curTask = ''
        console.log(this.todoLists)
      }
    },
    finishClick (index) {
      this.todoLists[index].isFinished = !this.todoLists[index].isFinished
    },
    deleteClick (index) {
      this.todoLists[index].isShow = false
    }
  }
}
</script>
<style>
.todo-main {
  margin: 10rpx 20rpx;
}
.todo-title {
  padding: 100rpx 0 50rpx 0;
  display: flex;
  flex-direction: column;
  align-items: center
}
.form-item {
  display: flex;
  flex-direction: row;
  height: 50rpx;
  line-height: 50rpx;
  padding: 10rpx 20rpx 16rpx 20rpx;
  border-bottom: 1px solid #EFEFEF;
}
.form-item-left {
  font-size: 30rpx;
  display: inline-block;
  width: 120rpx;
  font-weight: normal
}
.form-item-right {
  font-size: 30rpx;
  display: inline-block;
  position: relative;
  width: 580rpx;
}
.form-item-right-input {
  display: inline-block;
  border: none;
  padding-left: 0px;
  position: absolute;
  background-color: transparent;
  line-height: 50rpx;
  width: 450rpx;
  left: 0px;
  font-size: 28rpx;
}
.form-item-right-add {
  display: inline-block;
  color: #1AAD19;
  font-size: 30rpx;
  position: absolute;
  right: 0;
  border-left: 1px solid #ccc;
  line-height: 50rpx;
  padding-left: 20rpx;
  font-weight: bolder
}

/* 任务列表 */
.todo-list {
  margin: 30rpx 20rpx;
}

.todo-list-item {
  display: flex;
  flex-direction: row;
  height: 50rpx;
  line-height: 50rpx;
  font-size: 30rpx;
}

.todo-icon-body {
  display: inline-block;
  width: 50rpx;
}

.todo-list-item-task {
  width: 450rpx;
  font-size: 28rpx;
  overflow: hidden;
}

.task-finish {
  text-decoration: line-through
}

.todo-icon-check {
  width: 90rpx;
  display: inline-block;
  text-align: center;
  border-right: 1px solid #cccccc;
}

.todo-icon-delete {
  width: 90rpx;
  display: inline-block;
  text-align: center;
  font-weight: bolder;
}

.isFinished {
  color: #1AAD19;
  font-weight: bolder
}

.delete-style {
  width: 30rpx;
  height: 30rpx;
}
</style>
