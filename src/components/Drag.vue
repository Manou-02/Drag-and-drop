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

    function startDrag(event, item){
        event.dataTransfer.dropEffect = 'move';
        event.dataTransfer.effectAllowed = "move";

        event.dataTransfer.setData("itemId", item.id);
    }

    function onDrop(event){
        // const itemId = event.dataTransfer.getData('itemId');
        // const item = list.value.find(item => item.id === itemId);
        console.log("event\n", event);  
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