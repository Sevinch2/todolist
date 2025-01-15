<template>
    <ul>
<li>
    <button @click="$emit('complete')"
    v-bind:class="className">
    <i class="far fa-circle"></i>
    {{ task.title }}
</button>
    <button @click="$emit('remove')"><i class="far fa-trash-alt">
        <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=delete" />
        <span class="material-symbols-outlined">
delete
</span>
    </i></button>
</li>
</ul>
</template>
<script>
export default{
    name:"TaskItem",
    props:["task"],
    computed: {
        className() {
            let classes = ["toggle"];
            if(this.task.completed) {
                classes.push("toggle-completed");
            }
            return classes;
        }
    },
};
</script>
<style>
li{
    display: flex;
    justify-content: space-between;
    margin: 0 0 20px;
    display: list-item;
    text-align: -webkit-match-parent;
    unicode-bidi: isolate;
}
ul{
    margin: 0;
    padding: 0;
    list-style-type: disc;
}
button{
    cursor: pointer;
    font: 15px / 1.4 Poppins, sans-serif;
    color: #555;
    transition: all .3s linear;
    background: none;
    border: none;
}
</style>