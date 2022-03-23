<template>
    <div>
        <div v-if="step === 0">
            <Post v-for="(post, i) in post_data" :key="i" :post=post />
        </div>

        <!-- 필터선택페이지 -->
        <div v-else-if="step === 1">
            <div class="upload-image" :style="{backgroundImage: 'url('+ imgURL[index] +')'}"></div>
            <div class="filters">
                <div class="filter-1" @click="index = i" v-for="(img, i) in imgURL" :key="i" :style="{backgroundImage: 'url('+ imgURL[i] +')'}"></div>
            </div>
        </div>

        <!-- 글작성페이지 -->
        <div v-else-if="step === 2">
            <div class="upload-image"></div>
            <div class="write">
                <textarea class="write-box">write!</textarea>
            </div>
        </div>
    </div>
</template>

<script>
import Post from './Post.vue'

export default {
    props: [
        'post_data',
        'step',
        'imgURL'
    ],
    components: {
        Post,
    },
    data(){
        return {
            index: 0,
        }
    }
}
</script>

<style>
.upload-image{
width: 100%;
height: 450px;
background-size : cover;
}
.filters{
overflow-x:scroll;
white-space: nowrap;
}
.filter-1 {
width: 100px;
height: 100px;
margin: 10px 10px 10px auto;
padding: 8px;
display: inline-block;
color : white;
background-size: cover;
}
.filters::-webkit-scrollbar {
height: 5px;
}
.filters::-webkit-scrollbar-track {
background: #f1f1f1; 
}
.filters::-webkit-scrollbar-thumb {
background: #888; 
border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
background: #555; 
}
.write-box {
border: none;
width: 90%;
height: 100px;
padding: 15px;
margin: auto;
display: block;
outline: none;
}
</style>