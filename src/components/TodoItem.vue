<template>
  <div class="task-list-item">
    <font-awesome-icon icon="check-circle" @click="completeTask(todo)" :class="statusClasses" class="complete" />
    <input class="input" 
           :class="statusClasses" 
           type="text" 
           v-model="text">
    <font-awesome-icon icon="trash-alt" class="remove-btn" @click="remove"/>
  </div>
</template>

<script>

export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      default: () => ({
        text: "",
        isCompleted: false,
      })
    },
  },
  data: () => ({
    text: ""
  }),
  computed: {
    statusClasses() {
      return this.todo.isCompleted ? 'isCompleted' : '';
    }
  },
  methods: {
    remove() {
      this.$emit("remove", this.todo);
    },
    updateText(newText) {
      this.$emit("updateText", newText);
    },
    completeTask(todo) {
      this.$emit("taskCompleted", todo);
    }
  },
  watch: {
    todo: {
      handler(value) {
        if (this.text === value.text) {
          return;
        }
        this.text = value.text;
      },
      deep: true,
      immediate: true
    },
    text: {
      handler(value) {
        this.updateText(value);
      }
    }
  }
}
</script>

<style scoped>

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


.task-list-item {
  background-color: rgba(255, 255, 255, 0.7);
  display: flex;
  align-items: center;
  padding: 10px;
  border-radius: 35px;
  margin-bottom: 12px;
}

.remove-btn {
  margin-left: auto;
  margin-right: 5px;
  display: block;
  width: 16px;
  height: 16px;
  cursor: pointer;
}

.isCompleted {
  text-decoration: line-through;
}

</style>
