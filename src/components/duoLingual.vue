<template>
  <div  class="">
    <button @click="changeLanguageENG()">ENG</button>
    <button @click="changeLanguageSRB()">SRB</button>
    <ul>
      <li v-for="video in info" 
      v-bind:key="video.youtubeId">      
      <img :src="generateThumbnailUrl(video.youtubeId)" alt="">
      <a href="">{{video.title}}</a>

     </li>
    </ul>

    </div>
</template>

<script>

export default {
  name: 'duoLingual',
  data(){
    return{ 
        info:[],
        url:'https://api.myjson.com/bins/13mms5',
        urlSRB: "https://api.myjson.com/bins/99ixh",
        urlENG: "https://api.myjson.com/bins/13mms5"
    }
  },
mounted(){

if(agCookie.read("language") === "english"){
  this.axios.get(this.urlENG).then(response => {
  this.info = response.data.videos;
      
    })}else{
  this.axios.get(this.urlSRB).then(response => {
  this.info = response.data.videos;
      
    })}





},
methods:{

    generateThumbnailUrl(id){
      return youtube.generateThumbnailUrl(id)
    },
    createCookie(name, value, days){
      agCookie.create(name,value,days);
    },
     readCookie(name){
      return agCookie.read(name);
    },
    changeLanguageSRB(){
      this.url = this.urlSRB;
      this.axios.get(this.url).then(response => {
      this.info = response.data.videos;
        })
       agCookie.create("language","serbian",10);


    },
    changeLanguageENG(){
    this.url = this.urlENG;
     this.axios.get(this.url).then(response => {
      this.info = response.data.videos;
        })
      agCookie.create("language","english",10);


    }

}

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
div{
  padding-left: 50px;
  button{
    margin: 30px 0;
    background: #E71D36;
    border: none;
    color: #fff;
    margin-left: 5px;
    padding: 10px 20px;
    &:hover {
      background: darken($color: #273043, $amount: 10)
    }

  }
  ul{
    list-style-type: none;
     text-align: left;
     padding: 0;

     li{
       display: flex;
       align-items: center;
       margin-bottom: 20px;
       background: #EFF6EE;
       width: 60%;
       transition: 0.5s all;
       &:hover{
         border: 6px solid #E71D36;
       }
       &:hover a{
         text-decoration: underline;

       }
       a{
         margin-left: 50px;
         color: #E71D36;
         text-decoration: none;
         font-weight: bold;
         font-size: 20px;
         
       }

       
       img{
         width: 150px;
         border: 2px solid #E71D36;
       }
     }

  }
}

</style>
