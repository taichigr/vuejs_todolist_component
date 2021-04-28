<template>
  <div id="app">
    <div class="main-wrapper">
        <header>
            <h1>TODOリスト</h1>
            <p>入力したTODOは「未完了のTODO」に追加されます。<br>
            </p>
        </header>
        <main>
            <div class="input-area">
                <h2>入力エリア</h2>
                <input 
                  type="text" 
                  :value="inputText" 
                  @input="input($event)" 
                  placeholder="todoを入力"
                >
                <button :class="buttonStyle" @click="todoAdd">追加</button>
            </div>


            <div class="incomplete-area">
                <h2>未完了のTODO</h2>
                <ul v-for="list in incompleteTodos" :key="list">
                  <li>{{ list }}</li>
                  <button @click="moveToComplete(list)">完了へ</button>
                  <button @click="moveToHoryu(list)">保留へ</button>
                  <button @click="deleteIncompleteTodos(list)">削除</button>
                </ul>
            </div>


            <div class="complete-area">
                <h2>完了のTODO</h2>
                <ul v-for="list in completeTodos" :key="list">
                  <li>{{ list }}</li>
                  <button @click="deleteCompleteTodos(list)">削除</button>
                </ul>
            </div>

            <div class="horyu-area">
                <h2>保留中のTODO</h2>
                <ul v-for="list in horyuTodos" :key="list">
                  <li>{{ list }}</li>
                  <button @click="moveToIncompleteTodos(list)">未完了のTODOへ</button>
                  <button @click="deleteHoryuTodos(list)">削除</button>
                </ul>
            </div>
        </main>


    </div>
    <footer>
        Copyright taichi All Rights Reserved
    </footer>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  },
  data(){
    return {
      inputText: '',
      incompleteTodos: [],
      completeTodos: [],
      horyuTodos: [],
      isEditing: false
    }
  },
  computed: {
    buttonStyle() {
      const buttonStyle = []
      if(this.isEditing) {
        buttonStyle.push('active')
      }
      return buttonStyle
    }
    },
  methods: {
    input($event) {
      this.inputText = $event.target.value
      if(this.inputText !== ''){
        this.isEditing = true
      }else{
        this.isEditing = false
      }
    },
    todoAdd() {
      if(this.inputText !== ''){
        this.incompleteTodos.push(this.inputText)
        this.inputText = ''
        this.isEditing = false
      }
    },
    moveToComplete(list) {
      this.completeTodos.push(list)
      this.incompleteTodos.splice(list, 1)
    },
    moveToHoryu(list) {
      this.horyuTodos.push(list)
      this.incompleteTodos.splice(list, 1)
    },
    deleteIncompleteTodos(list) {
      this.incompleteTodos.splice(list, 1)
    },
    deleteCompleteTodos(list) {
      this.completeTodos.splice(list, 1)
    },
    moveToIncompleteTodos(list) {
      this.incompleteTodos.push(list)
      this.horyuTodos.splice(list, 1)
    },
    deleteHoryuTodos(list) {
      this.horyuTodos.splice(list, 1)
    }
  },
}
</script>


