<script setup>
import { ref, onUnmounted, onBeforeUnmount, onMounted } from 'vue';
const items = ref(
    JSON.parse(localStorage.getItem("todo.items")) || []
);
const addItem = () => {
    items.value.push(
        {
            id: items.value.length + 1,
            body: '',
            isDone: false
        }
    );
}
const removeItem = (id) => {
    items.value = items.value.filter(
        item => item.id !== id
    )
}

window.addEventListener("unload", () => {
    localStorage.setItem("todo.items", JSON.stringify(items.value));
    console.log("Saved!");
});
</script>

<template>
    <main>
        <div class="list-wrapper">
            <ul class="list">
                <li 
                class="list-item"
                v-for="item in items"
                :key="item.id">
                    <div class="list-item-div">
                    <input class="list-item-checkbox" type="checkbox" v-model="item.isDone">
                    <input class="list-item-input"
                    :class="{completed: item.isDone}" type="text" v-model="item.body">
                    <button class="list-item-removebtn" @click="removeItem(item.id)">X</button>
                    </div>
                </li>
                <li
                class="list-item-add"
                >
                    <button
                    class="list-item-addbtn"
                    @click="addItem()"
                    >
                        Add...
                    </button>
                </li>
            </ul>
        </div>
    </main>
</template>

<style>
    .list-wrapper {
        width: 50vw;
        min-width: 640px;
        background-color: #2e2e2e;
        border-radius: 15px;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-left: auto;
        margin-right: auto;
        padding-top: 1em;
    }
    .list {
        list-style-type: none;
        margin: 0;
        padding: 0;
        width: 100%;
    }
    .list-item {
        width: auto;
        margin-left: 20px;
        margin-right: 20px;
        margin-bottom: 20px;
    }
    .list-item-div {
        display: flex;
    }
    .list-item-checkbox {
        margin-right: 10px;
    }
    :checked {
        background-color:antiquewhite;
    }
    .list-item-input {
        width: calc(100% - 20px);
        font-size: 20px;
        background-color: unset;
        border-width: 0;
        border-bottom-width: 0.5px;
        color: #ffffff;
    }
    
    .completed {
        color: #23d023;
        text-decoration-line: line-through;
    }
    .list-item-removebtn {
        margin-left: 10px;
        background-color: #222222;
        border-width: 0;
        color: red;
        padding: 5px;
        border-radius: 5px;

    }
    .list-item-add {
        margin-left: 50px;
        margin-bottom: 20px;
    }
    .list-item-addbtn {
        font-size: 20px;
        background-color: #222222;
        border-width: 0;
        color: #ffffff;
        padding: 5px;
        border-radius: 5px;
    }

</style>