<template>
  <div id="app">

    <todo-header></todo-header>
    <todo-input v-on:addItemFunction="addOneItem"></todo-input>
    <todo-list v-bind:propsdata="items"></todo-list>
    <todo-footer></todo-footer>

  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  components: {
    'todo-header' : TodoHeader,
    'todo-input' : TodoInput,
    'todo-list' : TodoList,
    'todo-footer' : TodoFooter 
  },
  data: function() {
    return {
      items: []
    }
  },

  created : function() {
    if(localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        console.log("로컬스토리지 갯수 : " + localStorage.length);
        // stringify된 JSON 문자열을 다시 오브젝트로 변경
        this.items.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        // this.todoiItems.push(localStorage.key(i)));
        
      }
    } 
  },

  methods: {
    addOneItem(todoItem) {
      // input 컴포넌트에서 받은 인자값(item) 대입
      let obj = {
        completed: todoItem.completed,
        itemName: todoItem.itemName
      }; 

      window.localStorage.setItem(obj.itemName, JSON.stringify(obj));
      console.log(JSON.stringify(obj)); 

      this.items.push(obj);
    }
  }



}
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}

</style>