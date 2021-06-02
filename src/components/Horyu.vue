<template>
    <div class="horyu-area">
        <h2>保留中のTODO</h2>
        <ul v-for="(list, index) in horyuTodos" :key="list">
            <li>{{ list }}</li>
            <button @click="myMoveToIncompleteTodos(list, index)">未完了のTODOへ</button>
            <button @click="myDeleteHoryuTodos(list, index)">削除</button>
        </ul>
    </div>
</template>
<script>
export default {
    props: {
        horyuTodos: Array
    },
    data() {
        return {

        }
    },
    methods: {
        myMoveToIncompleteTodos(value, index) {
            this.$emit("my-move-to-incomplete-todos", value, index)
        },
        myDeleteHoryuTodos(value, index) {
            this.$emit("my-delete-horyu-todos", value, index)
        }
    }
}
</script>