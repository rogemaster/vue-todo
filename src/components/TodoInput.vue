<template>
    <div class="inputBox shdow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />
        <span class="addContainer">
            <i class="fas fa-plus addBtn" @click="addTodo"></i>
        </span>

        <Modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고!
                <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
            </h3>
            <div slot="body">입력한 값이 없습니다.</div>
        </Modal>
    </div>
</template>
 
<script>
import Modal from './common/Modal.vue';

export default {
    components: {
        Modal
    },

    data() {
        return {
            newTodoItem: '',
            showModal: false
        }
    },

    methods: {
        addTodo() {
            if(this.newTodoItem !== '') {
                this.$emit('addTodoItem', this.newTodoItem);
                this.clearInput();
            }else {
                this.showModal = !this.showModal;
            }
        },

        clearInput() {
            this.newTodoItem = '';
        }
    }
}
</script>

<style scoped>
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
    background: linear-gradient(to right, #6478f8, #8763f8);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
    cursor: pointer;
}
.closeModalBtn {
    color: #42b983;
}
 
</style>