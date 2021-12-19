<template>
    <div class="todo-footer">
        <label>
            <!-- <input type="checkbox" @click="$emit('allDone', allDone)"/> -->
            <input type="checkbox" @click="allDone" :checked="totalNumber==doneNumber"/>

        </label>
        <span>
            <span>已完成 {{ doneNumber }}</span> / 全部
            {{ todoList.length }}</span
        >
        <button class="btn btn-danger" @click="$emit('clear',clear())">清除已完成任务</button>
    </div>
</template>

<script>
export default {
    // 使用计算属性时不用相应更新？如果用updata则一直更新会进入死循环
    computed: {
        doneNumber: function () {
            let num = 0;
            this.todoList.forEach((todo) => {
                if (todo.done === true) num++;
            });
            return num;
        },
        totalNumber: function(){
            let num = 0;
            this.todoList.forEach(() => {
                num++;
                
            })
            return num
        }
    },
    methods: {
        //这样修改APP中每一项的值，没有破坏对props的引用，如果用新的数组直接赋值给props则会报错。
        clear() {
            let todoArr = [];
            this.todoList.forEach((val) => {
                if (val.done === false) todoArr.push(val);
            });
            return todoArr;
        },
        allDone(){
            this.todoList.forEach((val) => {
                val.done = !val.done;
            });
        }
    },
    props: ["todoList"],
};
</script>

<style>
/*footer*/
.todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
}

.todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
}

.todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
}

.todo-footer button {
    float: right;
    margin-top: 5px;
}
</style>
