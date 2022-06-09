<script setup>
import { ref } from 'vue';
const items = ref(
    []
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
</script>

<template>
    <main>
        <div class="list-wrapper">
            <ul class="list">
                <li 
                class="list-item"
                :class="{completed: item.isDone}"
                v-for="item in items"
                :key="item.id">
                    <div class="list-item">
                    <input type="checkbox" v-model="item.isDone">
                    <input class="list-item" type="text" v-model="item.body">
                    <button class="list-remove" @click="removeItem(item.id)">X</button>
                    </div>
                </li>
                <li
                class="list-item"
                >
                    <button
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
        font-size: 25px;
        display: flex;
        width: 100%;
    }
</style>