<template>
    <div v-if="posts.length > 0">
       <h3> Список пользователей </h3>
       <transition-group name="user-list">
        <PostItem 
            v-for="post in posts" 
            :post="post"
            :key='post.id' 
            @remove="$emit('remove', post)"
       />
       </transition-group>
    </div>
    <h2 v-else style="color: red">
    Список пользователей пуст
    </h2>
</template>

<script>
import PostItem from '@/components/PostItem';
export default {
    components: {PostItem},
    props: {
        posts: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style>
.user-list-item {
    display: inline-block;
    margin-right: 10px;
}

.user-list-enter-active,
.user-list-leave-active {
    transition: all 0.3s ease;
}

.user-list-enter-from,
.user-list-leave-to {
    opacity: 0;
    transform: translatex(130px);
}

.user-list-move {
    transition: transform 0.3s ease;
}
</style>