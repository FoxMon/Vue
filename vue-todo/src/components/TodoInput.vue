<template>
  <div class="inputBox shadow">
    <!-- v-on:keyup.enter 엔터 키 입력 시 이벤트 -->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo"/>
    <span class="addContainer" v-on:click="addTodo">add</span>
    <!-- use the modal component, pass in the prop -->
    <AlertModal v-if="showModal" @close="showModal = false">
      <!--
        you can use custom content here to overwrite
        default content
      -->
      <h3 slot="header">
        경고
        <span class="closeModalbtn" @click="showModal=false">close</span>
      </h3>
      <h4 slot="body">
        아무것도 입력하지 않았습니다.
      </h4>
    </AlertModal>
  </div>
</template>
<script>

import AlertModal from './common/AlertModal.vue';

export default {
  data: function() {
    return {
      newTodoItem: "",
      showModal: false,
    }
  },
  methods: {
    addTodo() {
      if(this.newTodoItem !== '') {
        // 버튼 클릭 or 엔터 입력 시, addTodoItem 상위 컴포넌트에 이벤트 발생 이 때 인자도 같이 올라감
        this.$emit('addTodoItem', this.newTodoItem)
        this.clearInput();
        this.showModal = false;
      } else {
        // 이질감이 있셈
        // alert("Input something");
        this.showModal = true;
      }
    },
    clearInput() {
      this.newTodoItem = "";
    }
  },
  components: {
    AlertModal: AlertModal,
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
.closeModalbtn {
  color: #42b983;
}
</style>
