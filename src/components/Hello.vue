<template>
  <div class="hello">
    <h2>Essential Links</h2>
    <div class="wrapper">
      <transition name="slide">
        <img :src=pics[nowIndex].src v-if="isShow">
      </transition>
      <transition name="slide-old">
        <img :src=pics[nowIndex].src v-if="!isShow" mode="out-in">
      </transition>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        nowIndex:0,
        isShow:true,
        pics:[
          {
            name:'pic6',
            src:require('../assets/img/ad6.jpg')
          },
          {
            name:'pic7',
            src:require('../assets/img/ad7.jpg')
          },
          {
            name:'pic8',
            src:require('../assets/img/ad8.png')
          },
          {
            name:'pic9',
            src:require('../assets/img/ad9.png')
          }
        ]
      }
    },
    computed:{
      nextIndex(){
        if(this.nowIndex === this.pics.length - 1){
          return 0
        }else {
          return this.nowIndex + 1
        }
      }
    },
    methods:{
      goto(index){
        this.isShow = false
        setTimeout(()=>{
          this.isShow = true;
          this.nowIndex = index
        },0)
      },

      runInv(){
        this.invId = setInterval(()=>{
          this.goto(this.nextIndex)
        },4000)
      }
    },

    mounted(){
      this.runInv();
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .slide-enter-active{
    transition: all .9s;
    /*transform: translateX(212px);*/
  }
  .slide-enter {
    transform: translateX(212px);
  }
  .slide-old-leave-active{
    transition:all 1s;
    transform: translateX(-212px);
  }
  .wrapper{
    width: 212px;
    height: 200px;
    border: 4px solid #ccc;
    margin: 0 auto;
    position: relative;
    overflow: hidden;
  }
  img{
    position: absolute;
    left: 0;
    top: 0;
    border: 1px solid red;
  }
</style>
