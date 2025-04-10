<template>
    <div class="navbar">
        <div @click="$router.push('/')">Vue</div>
        <div class="navbar_btns">
            <Mybutton @click="$router.push('/posts')">Посты</Mybutton>
            <Mybutton style="margin-left: 20px" @click="$router.push('/about')">О сайте</Mybutton>
            <Mybutton style="margin-left: 20px" @click="$router.push('/store')">store</Mybutton>
            <Mybutton style="margin-left: 20px" @click="$router.push('/composition')">Composition</Mybutton>
        </div>
    </div>
</template>


<script>
    export default {
        
    }
</script>

<style scoped>
.navbar {
    height: 50px;
    background-color: lightgrey;
    box-shadow: 2px 2px 4px gray;
    display: flex;
    align-items: center;
    padding: 0 15px;
}

.navbar_btns {
    margin-left: auto;
}
</style>