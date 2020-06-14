<template>
  <div class="head">
    <div class="head-toolbar d-flex justify-content-center">
      <div class="container-toolbar">
        <div v-for="( item, idx) in menu" :key="item.idx">
          <div>{{item.title}}</div>
          <div class="d-flex justify-content-center">
            <div v-if="idx == 0" class="dot-green"></div>
          </div>
        </div>
        <div class="ml-auto pa-20">
          <i class="fa fa-search curser-p" aria-hidden="true"></i>
        </div>
      </div>
    </div>
    <div class="slideshow-container">
      <div v-for="item in data" :key="item.idx" class="mySlides">
        <h1 class="control" style="margin-bottom:40px">{{item.title}}</h1>
        <div class="control" style="margin-bottom:76px">{{item.title}}</div>
        <img :src="item.image" alt />
      </div>
      <div class="control" style="text-align:center">
        <span class="dot-blue" @click="currentSlide(1)"></span>
        <span class="dot-blue" @click="currentSlide(2)"></span>
        <span class="dot-blue" @click="currentSlide(3)"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      slideIndex: 1,
      data: [],
      menu: []
    };
  },
  methods: {
    async getSliderData() {
      let response = await fetch(`https://voda-react-assessment.herokuapp.com/slider`);
      this.data = await response.json();
    },
    async getMenuData() {
      let response = await fetch(`https://voda-react-assessment.herokuapp.com/menu`);
      this.menu = await response.json();
    },
    currentSlide(n) {
      this.showSlides((this.slideIndex = n));
    },
    showSlides(n) {
      var slides = document.getElementsByClassName("mySlides");
      var dots = document.getElementsByClassName("dot-blue");
      if (n > slides.length) {
        this.slideIndex = 1;
      }
      if (n < 1) {
        this.slideIndex = slides.length;
      }
      for (let i = 0; i < slides.length; i++) {
        slides[i].style.display = "none";
        dots[i].className = dots[i].className.replace(" active", "");
      }
      slides[this.slideIndex - 1].style.display = "block";
      dots[this.slideIndex - 1].className += " active";
    }
  },
  async mounted() {
    await this.getSliderData();
    this.showSlides(1);
    this.getMenuData();
  }
};
</script>

<style scoped lang="less">
.head-toolbar {
  width: 100%;
  position: relative;
  background-color: #404859;
  z-index: 2;
  
}

.head {
  background-color: #404859;
  color: #ffffff;
  height: 366px;
}

.container-toolbar {
  display: flex;
  width: 550px;
  height: 82px;
}

.slideshow-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 284px;
}

.mySlides {
  display: none;
  text-align: center;
}

img {
  height: auto;
  position: absolute;
  z-index: 0;
  top: -380px;
  left: 0%;
  width: 100vw;
}

.control {
  z-index: 2;
  position: relative;
  text-shadow: 1px 1px 2px rgba(0,0,0,.7);
}
.dot-green {
  margin-top: 8px;
  height: 10px;
  width: 10px;
  background-color: rgb(89, 182, 154);
  border-radius: 50%;
  display: inline-block;
}

.dot-blue {
  cursor: pointer;
  height: 12px;
  width: 12px;
  margin: 2px;
  background-color: #bbbbbb00;
  border-radius: 50%;
  display: inline-block;
  border: 1px solid rgb(255, 255, 255);
  transition: background-color 0.6s ease;
   box-shadow: 1px 1px 2px rgba(0,0,0,.7);
  
}

.active,
.dot-blue:hover {
  background-color: #1191ed;
}
</style>