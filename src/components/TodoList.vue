<template>
  <div class="app-container">
    <h1 class="app-header">Todo Task List</h1>
    <todo-input-item @submit="onTopInputSubmit"></todo-input-item>
    <transition-group tag="ul" name="list" enter-from-class="animate__bounceOutDown" :enter-active-class=" 'animate_animated ' + addingAnimation" leave-to-class="animate__fadeOutRight">
      <template v-for="(item, i) in list" :key="i">
        <todo-item class="animate__animated" :todo="item" @remove="onTaskRemoved(i)" @taskCompleted="onTaskCompleted(i)"></todo-item>
      </template>
    </transition-group>
    <todo-input-item @submit="onBottomInputSubmit"></todo-input-item>
  </div>
</template>

<script>

import TodoInputItem from './TodoInputItem.vue';
import TodoItem from './TodoItem.vue';

const APPEND_ANIMATION = "animate__bounceInUp";
const PREPEND_ANIMATION = "animate__bounceInDown";

export default {
  name: 'TodoList',
  components: {
    TodoItem,
    TodoInputItem,
  },
  props: {
    modelValue: {
      type: Array
    },
  },
  data: () => ({
    addingAnimation: PREPEND_ANIMATION,
    list: []
  }),
  methods: {
    onTopInputSubmit(text) {
      this.addingAnimation = PREPEND_ANIMATION;
      this.prepend({
        text,
        isComplete: false,
      });
    },
    onBottomInputSubmit(text) {
      this.addingAnimation = APPEND_ANIMATION;
      this.append({
        text,
        isComplete: false,
      });
    },
    onTaskRemoved(i) {
      this.remove(i);
    },
    onTaskCompleted(index) {
      const task = this.copy(this.list[index]);
      task.isComplete = true;
      
      this.set(index, task);
    },
    save() {
      this.$emit('update:modelValue', Array.from(this.list));      
    },
    prepend(task) {
      this.list.splice(0, 0, task);
      this.save();
    },
    append(task) {
      this.list.push(task);
      this.save();
    },
    set(index, task) {
      this.list.splice(index, 1, task);
      this.save();
    },
    remove(index) {
      this.list.splice(index, 1);
      this.save();
    },
    copy(task) {
      return Object.assign({}, task);
    },
    isListDifferent(other) {
      if (other.length !== this.list.length) {
        return true;
      }

      return other.filter(x => !this.list.includes(x)).length > 0;
    }
  },
  watch: {
    modelValue: {
      handler(value) {        
        if (!Array.isArray(value)) {
          this.list = [];
          return;
        }

        if (!this.isListDifferent(value)) {
          return;
        }

        this.list = Array.from(value);
      },
      immediate: true
    }
  }
}
</script>

<style scoped>

.app-container{
  max-width: 480px;
  margin: auto;
  width: 100%;
  max-height: 100%;
  background-color: rgba(255,255,255, 0.3);
  padding: 25px;
  margin-bottom: 60px;
  border-radius: 25px;
  color: #222;
}

input{
  outline: none;
}

.app-header{
  font-size: 20px;
  line-height: 32px;
  margin: 0 0 12px 0;
  color: #272727;
}

.submit-task{
  margin: 7px 7px 0 7px;
  cursor: pointer;
}

.input {
  width: 100%;
  padding: 5px;
  outline: none;
  border: none;
  border-bottom: 1px solid #272727;
  margin: 0 9px;
  color: #272727;
  border-radius: 0;
}

.task-input {
  width: 100%;
  border: none;
  border-bottom: 1px solid #272727;
  background-color: transparent;
  border-radius: 0;
  color: #272727;
  box-shadow: none;
  padding: 10px;
  margin: -2px;
}

.task-input:focus {
   background-color: rgba(255, 255, 255, 0.7) ;
   border-radius: 35px;
   border: none;
   display: flex;
   align-items: center;
   padding: 22px;
}

.task-input::placeholder{
  color: #272727;
}

.task-list-item{
  background-color: rgba(255, 255, 255, 0.7);
  display: flex;
  align-items: center;
  padding: 10px;
  border-radius: 35px;
  margin-bottom: 12px;
}

.remove-btn{
  margin-left: auto;
  margin-right: 5px;
  display: block;
  width: 16px;
  height: 16px;
  cursor: pointer;
}

ul{ 
  list-style: none;
  padding: 0;
}

.isCompleted{
  text-decoration: line-through;
}


</style>
