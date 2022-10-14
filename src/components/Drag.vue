<script setup>
    import { ref } from "vue";

    const list = ref([
        {
            id: 0,
            name : "Zaza",
        },
        {
            id: 1,
            name : "Fafa",
        },
        {
            id: 2,
            name : "Gaga",
        },
    ]);

    const newList = ref([]);

    function startDrag(event, item){

        event.dataTransfer.setData("itemId", item.id);
    }

    function onDrop(event){
        const id = event.dataTransfer.getData('itemId');
        for(let i = 0; i < list.value.length; i++){
            if(list.value[i].id === +event.dataTransfer.getData('itemId')){
                newList.value = [...newList.value, list.value[i]]
            }
        }
    }
</script>

<template>
    <h3>Drag and Drop</h3>
    <div class="container">
        <div class="drag-container">
            <div 
                class="drag-item" 
                draggable="true" 
                v-for="item in list" 
                :key="item.id"
                @dragstart="startDrag($event, item)"
            >
                {{item.name}}
            </div>
        </div>

        <div 
            class="drop-container"
            @drop="onDrop($event)"
            @dragenter.prevent
            @dragover.prevent
        >
            <div 
                class="drag-item" 
                draggable="true" 
                v-for="item in newList" 
                :key="item.id"
                @dragstart="startDrag($event, item)"
            >
                {{item.name}}
            </div>
        </div>
    </div>
</template>

<style scoped >
    .container{
        display: flex;
        justify-content: center;
        gap: 30px;
        width: 80%;
    }
    .drag-container{
        background-color: rgb(208, 209, 209);
        padding: 10px;
        display: flex;
        flex-direction: column;
        gap: 20px;
        min-width: 200px;
    }

    .drag-item{
        background-color: white;
        padding: 10px;
        cursor: pointer;
    }
    .drop-container{
        background-color: rgb(208, 209, 209);
        padding: 10px;
        display: flex;
        flex-direction: column;
        gap: 20px;
        min-width: 200px;
    }
</style>