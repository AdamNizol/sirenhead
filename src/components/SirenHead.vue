<template>
  <div class="wrapper">
    <div class="container" :style="'width: '+size.width+'px; height: '+size.height+'px;'">
      <img class="fullHeight" src="@/assets/speakerBacks.png"/>

      <img :class="{'rightUpper': true, 'animateBiteRightUpper': biteRight}" src="@/assets/rightUpper.png"/>
      <img :class="{'rightLower': true, 'animateBiteRightLower': biteRight}" src="@/assets/rightLower.png"/>
      <div class="biteZoneRight" @mouseover="bite('right')" @mouseleave="resetBites()"></div>

      <img/>

      <img :class="{'leftUpper': true, 'animateBiteLeftUpper': biteLeft}" src="@/assets/leftUpper.png"/>
      <img :class="{'leftLower': true, 'animateBiteLeftLower': biteLeft}" src="@/assets/leftLower.png"/>
      <div class="biteZoneLeft" @mouseover="bite('left')"  @mouseleave="resetBites()"></div>

      <img/>

      <img class="fullHeight" src="@/assets/base.png"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SirenHead',
  data(){
    return {
      biteLeft: false,
      biteRight: false,
      maxWidth: window.innerWidth,
      maxHeight: window.innerHeight
    }
  },
  methods: {
    bite: function (direction){
      if(direction == "right"){
        this.biteRight = true;
      }else{
        this.biteLeft = true;
      }
      console.log("biting" + direction);
    },
    resetBites: function (){
      this.biteRight = false;
      this.biteLeft = false;
      console.log("stop biting");
    },
    resizeElem(){
      this.maxWidth = window.innerWidth;
      this.maxHeight = window.innerHeight;
    }
  },
  mounted() {
    window.addEventListener('resize', () => {
      this.resizeElem();
    })
  },
  computed: {
    size: function () {
      //let maxWidth = window.innerWidth;
      //let maxHeight = window.innerHeight;
      let ratio = 2480/3508;

      let width = 0;
      let height = 0;

      if( (this.maxWidth/this.maxHeight) > ratio ){
        height = this.maxHeight;
        width = height*(ratio);
      }else{
        width = this.maxWidth;
        height = width/ratio;
      }

      return {
        width: width,
        height: height
      };
    }
  },
}
</script>

<style scoped lang="scss">
@keyframes bodyAnimation {
  0% {
    transform: rotate(0deg) translateY(2%);
  }
  25% {
    transform: rotate(-2deg) translateY(1%);
  }
  50% {
    transform: rotate(0deg) translateY(2%);
  }
  75% {
    transform: rotate(2deg) translateY(1%);
  }
  100% {
    transform: rotate(0deg) translateY(2%);
  }
}

@keyframes biteRightLower {
  0% {
    right: 27%;
    transform: rotate(0deg);
  }
  50% {
    right: 21%;
    transform: rotate(30deg);
  }
  75% {
    right: 21%;
    transform: rotate(-15deg);
  }
  100% {
    right: 27%;
  }
}
@keyframes biteRightUpper {
  0% {
    right: 27%;
    transform: rotate(0deg);
  }
  50% {
    right: 21%;
    transform: rotate(-30deg);
  }
  75% {
    right: 21%;
    transform: rotate(15deg);
  }
  100% {
    right: 27%;
  }
}

.animateBiteRightLower {
  animation: biteRightLower 0.3s infinite;
}
.animateBiteRightUpper {
  animation: biteRightUpper 0.3s infinite;
}


@keyframes biteLeftLower {
  0% {
    left: 25%;
    transform: rotate(0deg);
  }
  50% {
    left: 19%;
    transform: rotate(-30deg);
  }
  75% {
    left: 19%;
    transform: rotate(15deg);
  }
  100% {
    left: 25%;
  }
}
@keyframes biteLeftUpper {
  0% {
    left: 25%;
    transform: rotate(0deg);
  }
  50% {
    left: 19%;
    transform: rotate(30deg);
  }
  75% {
    left: 19%;
    transform: rotate(-15deg);
  }
  100% {
    left: 25%;
  }
}

.animateBiteLeftLower {
  animation: biteLeftLower 0.3s infinite;
}
.animateBiteLeftUpper {
  animation: biteLeftUpper 0.3s infinite;
}


.biteZoneLeft, .biteZoneRight{
  position: absolute;
  z-index: 5;
  //border: 1px solid blue;
  &:hover{
    //cursor: pointer;
  }
}
.biteZoneRight{
  width: 12%;
  height: 8%;
  right: 22%;
  top: 13%;
}
.biteZoneLeft{
  width: 13%;
  height: 12%;
  left: 19.5%;
  top: 5.5%;
}

.wrapper {
  position: relative;
  display: flex;
  justify-content: center;
  overflow: hidden;
  background-color: rgb(45,45,45);
}
.container {
  animation: bodyAnimation 8s infinite;
  display: inline-block;
  position: relative;
  display: flex;
  justify-content: center;
  img {
    position: absolute;
  }
}
.fullHeight {
  height: 100%;
}
.rightLower, .rightUpper {
  height: 12%;
  right: 28%;
  top: 11.9%;
  transition: transform 4s ease-in-out;
}

.leftLower, .leftUpper {
  height: 13%;
  left: 25%;
  top: 6%;
}
</style>
