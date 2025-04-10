
<template>
    <div>
      <h1>Страница с постами</h1>
      <MyInput
        :model-value="searchQuery"
        placeholder="Поиск...."
        v-focus
      />
      <div class="app_btns">
        <MyButton
        >
          Создать пользователя
        </MyButton>
        <MySelect
          :model-value="selectedSort"
          :options="sortOptions"
        />
      </div>
      <MyDialog v-model:show="dialogVisible">
        <PostForm
        />
      </MyDialog>
      <PostList
        :posts="sortedAndSearchedPosts"
        v-if="!isPostsLoading"
      />
      <div v-else>Идет загрузка...</div>
    </div>
  </template>
  
  <script>
  import PostForm from '@/components/PostForm.vue';
  import PostList from "@/components/PostList.vue";
  import MyButton from "@/components/UI/MyButton.vue";
  //  import axios from 'axios';
  import MySelect from "@/components/UI/MySelect.vue";
  import MyInput from "@/components/UI/MyInput.vue";
  // import {ref} from 'vue'
  
  import {usePosts} from "@/hooks/usePosts.js";
  import useSortedPosts from "@/hooks/useSortedPosts.js";
  import useSortedAndSearchedPosts from "@/hooks/useSortedAndSearchedPosts.js";

  export default {
    components: {
      MyInput,
      MySelect,
      MyButton,
      PostList, PostForm
    },
    data() {
      return {
        dialogVisible: false,
        sortOptions: [
          {value: 'title', name: 'По названию'},
          {value: 'body', name: 'По содержимому'},
        ]
      }
    },
    setup() {
      const {posts, totalPages, isPostsLoading} = usePosts(10);
      const {sortedPosts, selectedSort} = useSortedPosts(posts);
      const {searchQuery, sortedAndSearchedPosts} = useSortedAndSearchedPosts(sortedPosts)
  
      return {
        posts,
        totalPages,
        isPostsLoading,
        sortedPosts,
        selectedSort,
        searchQuery,
        sortedAndSearchedPosts,
      }
    }
  }
  </script>
  
  <style>
  
  .app_btns {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
  }
  .page_wrapper {
    display: flex;
    margin-top: 15px;
  }
  .page {
    border: 1px solid black;
    padding: 10px;
  }
  .current-page {
    border: 2px solid teal;
  }
  
  .observer {
    height: 30px;
    background: green;
  }
  </style>