<template>
    <div >
    
        <h1>Страница с постами</h1>
        <MyInput 
        v-model="searchQuery" 
        placeholder="Поиск...." 
        v-focus 
        />
        <div class="app_btns">
            <MyButton 
            @click="showDialog"
            >
                Создать пользователя
            </MyButton>

            <MySelect 
            v-model="selectedSort" 
            :options="sortOptions"
            />

        </div>
        <MyDialog v-model:show="dialogVisible">

            <PostForm 
            @create="createPost" 
            />

        </MyDialog>

        <PostList 
        :posts="sortedAndSearchPosts" 
        @remove="removePost" 
        v-if="!isPostsLoading" 
        />
        <div v-else>Идет загрузка...</div>
        <div v-intersectoin="loadMorePosts" class="observer"></div>
        <!-- <div class="page_wrapper">
            <div v-for="pageNumber in totalPages" :key="pageNumber" class="page" :class="{ 'current-page': page == pageNumber
            }" 
            >
            {{ pageNumber }}
        </div>
        </div> -->
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyButton from "@/components/UI/MyButton";
import axios from 'axios';
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";

export default {
    components: {
        MyInput,
        MySelect,
        MyButton,
        PostList, PostForm
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                { value: 'title', name: 'По названию' },
                { value: 'body', name: 'По содержимому'},
            ]
        }
    },
    methods: {
        creatPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },

        // changePage(pageNumber) {
        //     this.page = pageNumber
        // },
        async fetchPosts() {
            try {
                this.isPostLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                });
                // if (response.status == 200) {
                this.totalPages = Math.ceil(response.headers['x-total-count'] /  this.limit)
                this.posts = response.data;
                // }
                // else {
                //     console.log('ytn jndtnf');
                // }
                // // }, 1000)
            } catch (e) {
                alert('Ошибка')
            } finally {
                this.isPostLoading = false;
            }
        },
        async loadMorePosts() {
            try {
                this.page += 1;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit
                    }
                });
                // if (response.status == 200) {
                this.totalPages = Math.ceil(response.headers['x-total-count'] /  this.limit)
                this.posts = [...this.posts, ...response.data];
            } catch (e) {
                alert('Ошибка')
            } 
        }
    },
    mounted() {
        this.fetchPosts();
        // console.log(this.$refs.observer);
        // const options = {
        //     rootMargin: '0px',
        //     threshold: 1.0
        // }
        // const callback = (entries, observer) => {
        //     if (entries[0].isIntersecting && this,page < this.totalPagesnn) {
        //         this.loadMorePosts()
        //     }
        // };
        // const observer = new IntersectionObserver(callback, option);
        // observer.observe(this.$refs.observer);
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
            )
        }
    },
    watch: {
        // page() {
        //     this.fetchPosts()
        // }
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
