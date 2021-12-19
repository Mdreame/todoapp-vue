<template>
    <div class="todo-footer" v-show="totalNumber">
        <label>
            <!-- <input type="checkbox" @click="$emit('allDone', allDone)"/> -->
            <!-- <input
                type="checkbox"
                @click="allDone"
                :checked="totalNumber == doneNumber"
            /> -->
            <!-- 这里全选和取消功能放在一起在结构上比较合理 -->
            <input
                type="checkbox"
                v-model="isAll"
            />
        </label>
        <span>
            <span>已完成 {{ doneNumber }}</span> / 全部
            {{ totalNumber }}
        </span>
        <!-- <button class="btn btn-danger" @click="$emit('clear',clear())">清除已完成任务</button> -->
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
    </div>
</template>

<script>
export default {
    props: ["todoList", "clearAllTodo","checkAllTodo"],

    // 使用计算属性时不用相应更新？如果用updata则一直更新会进入死循环
    computed: {
        doneNumber: function () {
            let num = 0;
            this.todoList.forEach((todo) => {
                if (todo.done === true) num++;
            });
            return num;
        },
        totalNumber() {
            return this.todoList.length;
        },
        isAll:{
            get(){
                return this.doneNumber === this.totalNumber;
            },
            set(val){
                this.checkAllTodo(val);
            }
        }
    },
    methods: {
        //这样修改APP中每一项的值，没有破坏对props的引用，如果用新的数组直接赋值给props则会报错。
        // clear() {
        //     let todoArr = [];
        //     this.todoList.forEach((val) => {
        //         if (val.done === false) todoArr.push(val);
        //     });
        //     this.clearAllTodo();
        //     return todoArr;
        // },
        // allDone() {
            
        // },
        clearAll() {
            console.log("clearAll called");
            
            this.clearAllTodo();
        },
    },
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
