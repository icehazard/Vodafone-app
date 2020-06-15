<template>
  <div class="head">
    <div class="head-toolbar d-flex justify-content-center">
      <div class="container-toolbar">
        <div v-for="(item, idx) in menu" :key="item.idx" class="navi-button">
          <div>{{ item.title }}</div>
          <div class="d-flex justify-content-center">
            <div v-if="idx == 0" class="dot-green"></div>
          </div>
        </div>
        <div class="ml-auto pa-20 navi-button" >
          <i class="fa fa-search curser-p" aria-hidden="true"></i>
        </div>
      </div>
    </div>
    <div v-for="(item, idx) in data" :key="item.idx">
      <div v-if="idx == slideIndex" class="img-container">
        <div class="position-absolute">
          <h1 class="center mb-40">{{ item.title }}</h1>
          <div class="mb-70">{{ item.subtitle }}</div>
          <div class="d-flex justify-content-center">
            <span
              v-for="(item, idx) in data.length"
              :key="item.idx"
              class="dot-blue"
              :class="{ active: idx == slideIndex }"
              @click="slideIndex = idx"
            />
          </div>
        </div>
        <img :src="item.image" :alt="item.title" />
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
      menu: [],
    };
  },
  methods: {
    async getSliderData() {
      let response = await fetch(
        `https://voda-react-assessment.herokuapp.com/slider`
      );
      this.data = await response.json();
    },
    async getMenuData() {
      let response = await fetch(
        `https://voda-react-assessment.herokuapp.com/menu`
      );
      this.menu = await response.json();
    },
  },
  mounted() {
    this.getSliderData();
    this.getMenuData();
  },
};
</script>

<style scoped lang="less">

.navi-button {
  padding: 20px;
}

.head {
  background-color: #404859;
  color: #ffffff;
  height: 366px;
}

.head-toolbar {
  width: 100%;
  position: relative;
  background-color: #404859;
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
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
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

@media only screen and (max-width: 395px) {
  img {
    height: 100%;
    width: auto;
  }
}
</style>
