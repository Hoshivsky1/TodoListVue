<template>
    <div class="app">
        <h1 style="font-size: 25px; font-weight:600">Cторінка з постами</h1>
        <my-button
            @click="showDialog"
            style="margin: 15px 0px">
            Створити пост
        </my-button>
        <my-dialog v-model:show="dialogVisible">
            <post-form 
                @create='createPost'
            />
        </my-dialog>
        <post-list :posts="posts"
            @remove="removePost"
        />  
    </div>
</template>

<script>
import PostForm from './components/PostForm';
import PostList from '@/components/PostList';
import MyDialog from './components/UI/MyDialog.vue';
import MyButton from './components/UI/MyButton.vue';
export default {
    components: {
    PostList,
    PostForm,
    MyDialog,
    MyButton
},
    data() {
        return {
            posts: [
                { id: 1, title: "Javascript", body: "Опис поста" },
                { id: 2, title: "Javascript 2", body: "Опис поста 2" },
                { id: 3, title: "Javascript 3", body: "Опис поста 3" },
                { id: 4, title: "Javascript 3", body: "Опис поста 4" },
            ],
            dialogVisible: false
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
        }
    },
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
</style>
