<template>
    <div>
        <h4><strong>Створення поста</strong></h4>
        <form @submit.prevent>
            <my-input
                v-model="post.title"
                type="text"
                placeholder="Назва"
            />
            <my-input
                v-model="post.body"
                type="text"
                placeholder="Опис"
            />
            <my-button 
                style="align-self: flex-end"
                @click="createPost"
            >
                Create
            </my-button>
        </form>
    </div>
</template>
 
<script>
export default {
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
            this.post.id = Date.now();
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: '',
            }
        }
    }
}
</script>
 
<style scoped>
form {
    display: flex;
    flex-direction: column;
}

</style>