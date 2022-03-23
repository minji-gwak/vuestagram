<template>
  <div class="header">
    <ul class="header-button-left">
      <li @click="step--">Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li @click="step++">Next</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>
  <div class="tab-box">
    <span class="tab" @click="step = 0">1</span>
    <span class="tab" @click="step = 1">2</span>
    <span class="tab" @click="step = 2">3</span>
  </div>

  <Container :post_data=postData :step=step :imgURL=imgURL />
  <button @click="getData()">더보기</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" multiple />
      <label for="file" class="input-plus">+</label>
    </ul>
 </div>
</template>

<script>
import Container from './components/Container.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Container
  },
  methods: {
      getData() {
        axios.get('https://codingapple1.github.io/vue/more' + this.cnt + '.json').then( result => {
          console.log('result.data : ', result.data)
          this.postData.push(result.data)
          this.cnt++
        })
      },
      upload(e){
        let file = e.target.files;
        let url = URL.createObjectURL(file[0]);
        console.log(url);
        this.imgURL.push(url)
        this.step++
      }
    },
    data(){
      return {
        cnt: 0,
        step: 0,
        imgURL: [],
        postData: [],
        post_data: [
          {likes: 43, name: 'mi_xx2', content: 'Hello', date: 'June 6'},
          {likes: 17, name: 'food.tomorrow', content: 'How are you', date: 'July 15'},
          {likes: 32, name: 'j_mahaph', content: 'this is me', date: 'October 30'},
        ]
      }
    },

    setup(){
    },

    created(){
        this.getData()
    }
}
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.tab-box {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  margin-bottom: 20px;
}
.tab {
  text-align: center;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
