<template>
    <form @submit.prevent>
        <h4>Создание поста</h4>
        <MyInput 
            v-focus
            v-model="post.title"
            type="text"
            placeholder="Название " 
        />
        <!-- @update:modelValue="(val) => console.log(val)" -->
        <MyInput 
            v-model="post.body"
            type="text" 
            placeholder="Описание "
        />
        <MyButton 
            class="btn"
            style="align-self: flex-end; margin-top: 15px;"
            @click="createPost"
        >
            Создать
        </MyButton>
    </form>
</template>

<script>
export default {
    // components: {
    //     MyButton
    // },
    data() {
        return {
            post: {
                title: '',
                body: ''
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now()
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: ''
            }
        }
    },
}
</script>

<style scoped>
form {
    display: flex;
    flex-direction: column;
    border-radius: 4px;
}
</style>