<template>
    <button class="btn">
        <slot></slot>            
    </button>
</template>

<script>
export default {
    name: 'MyButton',
}
</script>

<style>
.btn {
    color: teal;
    padding: 10px 15px;
    background: none;
    border: 1px solid teal;
    border-radius: 4px;
}
</style> 