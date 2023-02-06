<template>
  <div>
    <ul>
      <li v-for="(item, index) in items" v-bind:key="item.itemName" class="shadow">
        <i class="fas fa-check checkBtn" v-bind:class="{checkBtnCompleted: item.completed}" 
           v-on:click="toggleComplete(item)"></i>
        <span v-bind:class="{textCompleted: item.completed}">{{ item.itemName }}</span>
        <span class="removeBtn" v-on:click="removeTodo(item, index)" >
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
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
    removeTodo(item, index){
      console.log(JSON.stringify(item));
      localStorage.removeItem(localStorage.key(index));
      this.items.splice(index, 1);
      
    },
    toggleComplete(item){
      // 화면에서 상태 갱신
      item.completed = !item.completed;
      // 로컬스토리지에서 데이터 갱신
      localStorage.removeItem(item.itemName);
      localStorage.setItem(item.itemName, JSON.stringify(item));
      
      //let item = localStorage.getItem(localStorage.key(index));
    }
  }

}
</script>

<style scoped>
ul {
  list-style-type: none; /* li의 점 삭제 */
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}


</style>