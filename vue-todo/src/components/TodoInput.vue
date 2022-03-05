<template>
  <div class="inputBox shadow">
    <!-- v-on:keyup.enter 엔터 키 입력 시 이벤트 -->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo"/>
    <span class="addContainer" v-on:click="addTodo">add</span>
  </div>
</template>
<script>
export default {
  data: function() {
    return {
      newTodoItem: "",
    }
  },
  methods: {
    addTodo: function() {
      if(this.newTodoItem !== '') {
        // 버튼 클릭 or 엔터 입력 시, addTodoItem 상위 컴포넌트에 이벤트 발생 이 때 인자도 같이 올라감
        this.$emit('addTodoItem', this.newTodoItem)
        this.clearInput();
      }
    },
    clearInput: function() {
      this.newTodoItem = "";
    }
  }
}
</script>
<style>
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
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>
