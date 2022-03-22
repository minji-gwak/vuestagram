<template>
    <div>
        <Post v-for="(post, i) in post_data" :key="i" :post=post />
    </div>
</template>

<script>
import Post from './Post.vue'

export default {
    props: [
        'post_data'
    ],
    components: {
        Post,
    },
}
</script>