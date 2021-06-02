<template>
  <div id="app">
    <div class="main-wrapper">
      <header>
        <h1>TODOリスト</h1>
        <p>入力したTODOは「未完了のTODO」に追加されます。<br>
        </p>
      </header>
      <main>
        <!-- インプットエリア -->
        <Input 
          :inputText="inputText" 
          :isEditing="isEditing" 
          @myInput="myInput($event)" 
          @myInputAdd="myInputAdd"
        />

        <!-- 未入力エリア -->
        <Incomplete 
          :incompleteTodos="incompleteTodos"
          @my-move-to-complete="myMoveToComplete"
          @my-move-to-horyu="myMoveToHoryu"
          @my-delete-incomplete-todos="myDeleteIncompleteTodos"
        />

        <!-- 完了エリア -->
        <Complete 
          :completeTodos="completeTodos"
          @my-delete-complete-todos="myDeleteCompleteTodos"
        />


        <!-- 保留エリア -->
        <Horyu 
          :horyuTodos="horyuTodos"
          @my-move-to-incomplete-todos="myMoveToIncompleteTodos"
          @my-delete-horyu-todos="myDeleteHoryuTodos"
        />
      </main>


    </div>
    <footer>
      Copyright taichi All Rights Reserved
    </footer>
  </div>
</template>

<script>
import Complete from './components/Complete.vue'
import Horyu from './components/Horyu.vue'
import Incomplete from './components/Incomplete.vue'
import Input from "./components/Input"
  export default {
    name: 'App',
    components: {
      Input,
      Incomplete,
      Complete,
      Horyu,
    },
    data() {
      return {
        inputText: '',
        incompleteTodos: [],
        completeTodos: [],
        horyuTodos: [],
        isEditing: false
      }
    },
    computed: {},
    methods: {
      //カスタムイベント
      myInput($event){
        this.input($event)
      },
      myInputAdd(text) {
        this.todoAdd(text)
      },
      myMoveToComplete(value, index) {
        this.moveToComplete(value, index)
      },
      myMoveToHoryu(value, index) {
        this.moveToHoryu(value, index)
      },
      myDeleteIncompleteTodos(value, index) {
        this.deleteIncompleteTodos(value, index)
      },
      myDeleteCompleteTodos(value, index) {
        this.deleteCompleteTodos(value, index)
      },
      myMoveToIncompleteTodos(value, index) {
        this.moveToIncompleteTodos(value, index)
      },
      myDeleteHoryuTodos(value, index) {
        this.deleteHoryuTodos(value, index)
      },
      //メソッド
      input($event) {
        this.inputText = $event.target.value
        if (this.inputText !== '') {
          this.isEditing = true
        } else {
          this.isEditing = false
        }
      },
      todoAdd(text) {
        if (text !== '') {
          this.incompleteTodos.push(text)
          this.inputText = ''
          this.isEditing = false
        }
      },
      moveToComplete(value, index) {
        this.completeTodos.push(value)
        this.incompleteTodos.splice(index, 1)
      },
      moveToHoryu(value, index) {
        this.horyuTodos.push(value)
        this.incompleteTodos.splice(index, 1)
      },
      deleteIncompleteTodos(value, index) {
        this.incompleteTodos.splice(index, 1)
      },
      deleteCompleteTodos(value, index) {
        this.completeTodos.splice(index, 1)
      },
      moveToIncompleteTodos(value, index) {
        this.incompleteTodos.push(value)
        this.horyuTodos.splice(index, 1)
      },
      deleteHoryuTodos(index) {
        this.horyuTodos.splice(index, 1)
      },
    },
  }
</script>