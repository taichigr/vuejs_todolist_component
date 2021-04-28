<template>
    <div class="horyu-area">
        <h2>保留中のTODO</h2>
        <ul v-for="list in horyuTodos" :key="list">
            <li>{{ list }}</li>
            <button @click="myMoveToIncompleteTodos(list)">未完了のTODOへ</button>
            <button @click="myDeleteHoryuTodos(list)">削除</button>
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
        myMoveToIncompleteTodos(value) {
            this.$emit("my-move-to-incomplete-todos", value)
        },
        myDeleteHoryuTodos(value) {
            this.$emit("my-delete-horyu-todos", value)
        }
    }
}
</script>