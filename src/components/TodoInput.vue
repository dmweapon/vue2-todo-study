<template>
  <div class="inputBox shadow">
    <input type="text" v-model="item.itemName" v-on:keyup.enter="addTodo()">
    <!-- <button v-on:click="addTodo()">add</button> -->
    <span class="addContainer" v-on:click="addTodo()"> 
       <i class="fas fa-plus addBtn"></i> 
    </span>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      item: {
        completed: false,
        itemName: ""
      }
    };
  },
  methods: {
    addTodo() {
      if(this.item.itemName !== ''){
        //let obj = this.item;
        let obj = {
          completed: this.item.completed,
          itemName: this.item.itemName
        }
        window.localStorage.setItem(obj.itemName, JSON.stringify(obj));
        console.log(JSON.stringify(this.item));
        this.clearInput();
      }
      
    },
    clearInput() {
      this.item.itemName = "";
    },
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0.5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>
