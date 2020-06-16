<template>
  <div class="head">
    <div class="head-toolbar d-flex justify-content-center">
      <div class="container-toolbar">
        <button v-for="(item, idx) in menu" :key="item.idx" class="navi-button">
          <div>{{ item.title }}</div>
          <div class="d-flex justify-content-center">
            <div v-if="idx == 0" class="dot-green"></div>
          </div>
        </button>
        <div class="ml-auto pa-20 navi-button mt-2">
          <i class="fa fa-search" aria-hidden="true"></i>
        </div>
      </div>
    </div>
    <div id="carousel" class="carousel slide" data-ride="carousel">
      <div class="carousel-inner">
        <div v-for="(item, idx) in data" :key="item.idx" class="carousel-item" :class="{ active: idx == 0 }">
          <div class="img-container">
            <div class="position-absolute">
              <h1 class="center mb-40">{{ item.title }}</h1>
              <h5 class="mb-70">{{ item.subtitle }}</h5>
              <div class="d-flex justify-content-center">
                <div
                  v-for="(item, subIndex) in data.length"
                  :key="item.subIndex"
                  data-target="#carousel"
                  class="dot-blue"
                  :class="{ active: idx == subIndex }"
                  :data-slide-to="subIndex"
                ></div>
              </div>
            </div>
            <img class="" :src="item.image" :alt="item.title" />
          </div>
        </div>
      </div>
      <a class="carousel-control-prev" href="#carousel" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a class="carousel-control-next" href="#carousel" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [],
      menu: [],
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
  },
  mounted() {
    this.getSliderData();
    this.getMenuData();

    $(".carousel").carousel({
      wrap: false,
      interval: 10000,
    });
  },
};
</script>

<style scoped lang="less">
.navi-button {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 14px;
  margin-left: 20px;
  border: none;
  background-color: rgba(0, 139, 139, 0);
  color: rgb(255, 255, 255);
  font-size: 20px;
}

.head {
  background-color: #404859;
  color: #ffffff;
  height: 366px;
  box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.1);
}

.head-toolbar {
  width: 100%;
  position: relative;
  box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.1);
  z-index: 1;
}

.container-toolbar {
  display: flex;
  width: 550px;
  height: 82px;
}

.img-container {
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  height: 284px;
  text-shadow: 2px 1px 6px rgb(94, 94, 94);
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
  margin: 5px;
  background-color: #bbbbbb00;
  border-radius: 50%;
  display: inline-block;
  border: 1px solid rgb(255, 255, 255);
  transition: background-color 0.6s ease;
  box-shadow: 2px 1px 2px rgba(0, 0, 0, 0.7);
}

.active,
.dot-blue:hover {
  background-color: #1191ed;
}

img {
  height: auto;
  width: 100%;
}

@media only screen and (max-width: 445px) {
  img {
    height: 100%;
    width: 100%;
  }
}

@media only screen and (max-width: 375px) {
  img {
    height: 100%;
    width: auto;
  }
}
</style>
