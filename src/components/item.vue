<template>
    <div id="app">
        <div style="" class="item-list">
            {{item.value}}
        </div>
    </div>
</template>
<script>
    export default {
        props:{
            item:Object
        }
    }
</script>
<style>
    .item-list{
        height: 40px;
        border: 1px solid red;
    }
</style>
