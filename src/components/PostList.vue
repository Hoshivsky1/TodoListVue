<template>
    <div v-if="posts.length > 0">
        <h3 style="font-size: 18px;"><strong>Cписок користувачів</strong></h3>
        <post-item 
            v-for="post in posts" 
            :key="post.id" 
            :post="post"
            @remove="$emit('remove', post)"/>
    </div>
    <h2 v-else style="color: red; font-size:20px">
        <strong>Список користувачів пустий</strong>
    </h2>
</template>
 
<script>
import PostItem from "@/components/PostItem";
export default {
    components:{
        PostItem
    },
    props: {
        posts: {
            type: Array,
            required: true
        }
    }
}
</script>
 
<style scoped>
</style>