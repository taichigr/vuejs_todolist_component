<template>
    <div class="incomplete-area">
        <h2>未完了のTODO</h2>
        <ul v-for="(list, index) in incompleteTodos" :key="list">
            <li>{{ list }}</li>
            <button @click="emitMoveToComplete(list, index)">完了へ</button>
            <button @click="emitMoveToHoryu(list, index)">保留へ</button>
            <button @click="emitDeleteIncompleteTodos(list, index)">削除</button>
        </ul>
    </div>
</template>
<script>
    export default {
        props: {
            incompleteTodos: Array
        },
        data() {
            return {

            }
        },
        methods: {
            emitMoveToComplete(value, index) {
                this.$emit("my-move-to-complete", value, index)
            },
            emitMoveToHoryu(value, index) {
                this.$emit('my-move-to-horyu', value, index)
            },
            emitDeleteIncompleteTodos(value, index) {
                this.$emit('my-delete-incomplete-todos', value, index)
            }
        }
    }
</script>