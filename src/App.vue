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
      myMoveToComplete(value) {
        this.moveToComplete(value)
      },
      myMoveToHoryu(value) {
        this.moveToHoryu(value)
      },
      myDeleteIncompleteTodos(value) {
        this.deleteIncompleteTodos(value)
      },
      myDeleteCompleteTodos(value) {
        this.deleteCompleteTodos(value)
      },
      myMoveToIncompleteTodos(value) {
        this.moveToIncompleteTodos(value)
      },
      myDeleteHoryuTodos(value) {
        this.deleteHoryuTodos(value)
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
      moveToComplete(value) {
        this.completeTodos.push(value)
        this.incompleteTodos.splice(value, 1)
      },
      moveToHoryu(value) {
        this.horyuTodos.push(value)
        this.incompleteTodos.splice(value, 1)
      },
      deleteIncompleteTodos(value) {
        this.incompleteTodos.splice(value, 1)
      },
      deleteCompleteTodos(value) {
        this.completeTodos.splice(value, 1)
      },
      moveToIncompleteTodos(value) {
        this.incompleteTodos.push(value)
        this.horyuTodos.splice(value, 1)
      },
      deleteHoryuTodos(value) {
        this.horyuTodos.splice(value, 1)
      },
    },
  }
</script>