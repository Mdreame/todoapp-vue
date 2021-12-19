<template>
    <div>
        <div class="todo-header">
            <!-- 这里写双引号将add括起来会报错：@keydown.enter="$emit("add", generateTodoItem)" -->
            <!-- $emit函数为父组件指定的关键词字符串v-on:<keyword>, 
                第二个参数可传递任意类型给父组件 
                父组件通过$event接受参数-->
            <input
                @keydown.enter="$emit('add', generateTodoItem())"
                v-model="detail"
                type="text"
                placeholder="请输入你的任务名称，按回车键确认"
            />
        </div>
    </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
    data() {
        return {
            detail: "",
            // 组件间通信：将todoList传递给List组件
            todoList: [],
        };
    },
    methods: {
        // addTdo() {
        //     if (this.detail !== "") {
        //         this.id++;
        //         const todoitem = {
        //             id: nanoid(),
        //             detail: this.detail,
        //             done: this.done,
        //         };

        //         console.log(todoitem);

        //         this.todoList.push(todoitem);
        //     }
        //     this.detail = "";
        // },

        //通过v-on来触发，给APP传生成的todo对象
        generateTodoItem() {
            //数据的校验
            if (!this.detail) return;
            const todoitem = {
                id: nanoid(),
                detail: this.detail,
                done: false,
            };
            // console.log(todoitem);
            this.detail = "";
            return todoitem;
        },
    },
};
</script>

<style>
/*header*/
.todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
}

.todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
        0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
