<template>
    <!-- 原来的写法 -->
    <!-- <ul class="todo-main">
        <ListItem
            v-for="todo in todolist"
            :key="todo.id"
            :detail="todo.detail"
            :done="todo.done"
            v-on:isDone="todo.done = !todo.done"
        ></ListItem>
    </ul> -->
    <!-- 改进后的写法：将整个对象传入，而不是分别赋值可以保持数据清晰简洁 -->
    <ul class="todo-main">
        <ListItem
            v-for="todo in todoList"
            :key="todo.id"
            :todo="todo"
            @isDone="gtd($event)"
            @removeItem="removeItem($event)"
        ></ListItem>
    </ul>
</template>

<script>
import ListItem from "./ListItem.vue";

export default {
    methods: {
        gtd(e) {
            //每点击一项，遍历数组找到该项，将其done值改为true
            // indexOf返回数组中匹配到的第一项索引，若没有则返回-1
            let index = this.todoList.indexOf(e);
            this.todoList[index].done = !this.todoList[index].done;
            //检测数组的更新：只有使用9个方法中的一个或者使用vue.set
            // this.todoList.splice(index, 1, e);
            
        },
        removeItem(e){
            let index = this.todoList.indexOf(e);
            // splice会引起数据更新
            this.todoList.splice(index, 1);
        }
    },
    components: {
        ListItem,
    },
    props: ["todoList"],
};
</script>

<style>
/*main*/
.todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
}

.todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
}
</style>
