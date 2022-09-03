<template>
    <div class="app">
        <h1 style="font-size: 25px; font-weight:600">Cторінка з постами</h1>
        <div class="app__btns">
            <my-button
                @click="showDialog"
            >
                Створити пост
            </my-button>
            <my-select
                v-model="selectedSort"
                :options="sortOptions"
            />
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form 
                @create='createPost'
            />
        </my-dialog>
        <post-list 
            :posts="sortedPosts"
            @remove="removePost"
            v-if="!isPostsLoading"
        />
        <div v-else>Іде загрузка...</div>  
    </div>
</template>

<script>
import PostForm from './components/PostForm';
import PostList from '@/components/PostList';
import MyDialog from './components/UI/MyDialog.vue';
import MyButton from './components/UI/MyButton.vue';
import axios from 'axios';
import MySelect from './components/UI/MySelect.vue';

export default {
    components: {
    PostList,
    PostForm,
    MyDialog,
    MyButton,
    MySelect
},
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По назві'},
                {value: 'body', name: 'По опису'},

            ]
        };
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                this.posts = response.data;
            } catch (e) {
                alert('Помилка')
            } finally {
                this.isPostsLoading = false;
            }
        }
    },
    mounted() {
        this.fetchPosts( )
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
            })
        }
    },
    watch: {
        // selectedSort(newValue) {
        //     this.posts.sort((post1, post2) => {
        //         return post1[newValue]?.localeCompare(post2[newValue])
        //     })
        // }
    }
};
</script>

<style>
* {
    padding: 0;
    margin: 0;
    border: 0;
}
*,
*:before,
*:after {
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
:focus,
:active {
    outline: none;
}
a:focus,
a:active {
    outline: none;
}
nav,
footer,
header,
aside {
    display: block;
}
html,
body {
    height: 100%;
    width: 100%;
    font-size: 100%;
    line-height: 1;
    font-size: 14px;
    -ms-text-size-adjust: 100%;
    -moz-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
}
input,
button,
textarea {
    font-family: inherit;
}
input::-ms-clear {
    display: none;
}
button {
    cursor: pointer;
}
button::-moz-focus-inner {
    padding: 0;
    border: 0;
}
a,
a:visited {
    text-decoration: none;
}
a:hover {
    text-decoration: none;
}
ul li {
    list-style: none;
}
img {
    vertical-align: top;
}
h1,
h2,
h3,
h4,
h5,
h6 {
    font-size: inherit;
    font-weight: inherit;
}

.app {
    padding: 20px;
}

.app__btns {
    margin: 15px 0px;
    display: flex;
    justify-content: space-between;
}
</style>
