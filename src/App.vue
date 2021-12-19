<template>
    <div id="app">
        <div class="todo-container">
            <div class="todo-wrap">
                <SearchBar @add="add($event)" />
                <List :todoList="todoList"></List>
                <Result
                    :todoList="todoList"
                    @clear="clear($event)"
                    @allDone="allDone($event)"
                ></Result>
            </div>
        </div>
    </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import List from "./components/List.vue";
import Result from "./components/Result.vue";

export default {
    name: "App",
    data() {
        return {
            todoList: JSON.parse(localStorage.getItem("todoList")) || [],
        };
    },
    watch: {
        todoList: {
            deep: true,
            handler(value) {
                localStorage.setItem("todoList", JSON.stringify(value));
            },
        },
    },
    methods: {
        add(e) {
            //如果输入框为空则不响应
            if (!e) return;
            this.todoList.unshift(e);
        },
        clear(e) {
            this.todoList = e;
        },
        allDone() {},
    },
    components: {
        SearchBar,
        List,
        Result,
    },
};
</script>

<style>
/*base*/
body {
    background: #fff;
}

.btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
        0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
}

.btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
}

.btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
}

.btn:focus {
    outline: none;
}

.todo-container {
    width: 600px;
    margin: 0 auto;
}
.todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
}
</style>
