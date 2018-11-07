<template>
<ul class="list">
    <li v-for="item in data" :key="item.id" :class="{complated:item.complated}" v-on:click="$emit('toggleTaskStatus',item.id)">
        <span>- </span>
        <span>{{item.name}}</span>
        <span class="remove" v-on:click="$emit('removeTask',item.id)">x</span>
    </li>
</ul>
</template>

<script>
export default {
    props:{
        data:{
            type:Array,
            required:true
        }
    },
}
</script>

<style>
.list{
    list-style: none;
    margin-top: 10px;
}
.list li{
    margin-bottom: 10px;
    padding:5px 0; 
}
.list li:hover{
    background: #eee;
}
.list li.complated{
    text-decoration: line-through;
}
.list .remove{
    float: right;
    padding: 2px 10px;
    color: red;
    cursor: pointer;
    line-height: 16px;
}
.list .remove:hover{
    font-weight: 600;
}
</style>
