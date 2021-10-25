<template>
  <div>
    <form action="" @submit.prevent.stop="submit">
      <div class="add-task">
       <input type="text" v-model="todo"
         id="input" 
         class="task-input">
      </div>
    </form>
  </div>
</template>

<script>

export default {
    name: 'TodoInputItem',
    props: {
      todos: {
        type: Array,
      },
    },
    data: () => ({
      todo: ""
    }),
    computed: {
      isValid() {
        if (typeof this.todo !== "string") {
          return false;
        }

        return !!this.todo.trim();
      }
    },
    methods: {
      submit() {
        if(! this.isValid){
          return;
        }

        this.$emit('submit', this.todo);
        this.todo = "";
        const input = document.querySelector('#input')
          input.blur(); 
      },
    }
}
</script>

<style scoped>


input{
  outline: none;
}

.app-header {
  font-size: 20px;
  line-height: 32px;
  margin: 0 0 12px 0;
  color: #272727;
}

.add-task {
  height: 40px;
  font-size: 14px;
  display: flex;
  padding: 15px 0;
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

</style>