<template>
    <div class="input-area">
        <h2>入力エリア</h2>
        <input type="text" :value="inputText" @input="input($event)" placeholder="todoを入力">
        <button :class="buttonStyle" @click="todoAdd">追加</button>
    </div>
</template>
<script>
    export default {
        props: {
            inputText: String,
            isEditing: Boolean
        },
        data() {
            return {}
        },
        computed: {
            buttonStyle() {
                const buttonStyle = []
                if (this.isEditing) {
                    buttonStyle.push('active')
                }
                return buttonStyle
            }
        },
        methods: {
            input($event) {
                this.$emit('myInput', $event)
            },
            todoAdd() {
                this.$emit('myInputAdd', this.inputText)
            }
        }
    }
</script>