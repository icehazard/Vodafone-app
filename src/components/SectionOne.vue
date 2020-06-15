<template>
  <div>
    <div class="grid-container">
      <div
        v-for="(item, idx) in data"
        :key="item.idx"
        class="img-container"
        :class="['item' + idx]"
      >
        <img :src="item.img" :alt="item.title" />
        <div v-if="idx == 1" class="center position-absolute">
          <i class="fa fa-eye curser-p" aria-hidden="true"></i>
          <div>{{ item.title }}</div>
          <div class="line"></div>
        </div>
      </div>
    </div>
    <div class="banner"></div>
  </div>
</template>

<script>
export default {
  props: ["data"],
};
</script>

<style scoped>
.grid-container {
  width: 1170px;
  height: 630px;
  display: grid;
  grid-template-areas:
    "aside nw ne "
    "aside sw se ";

  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  grid-gap: 30px;
  padding: 10px;
  color: white;
}

.img-container {
  background-color: #cccccc;
  text-align: center;
  padding: 0;
  font-size: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  overflow: hidden;
}

.img-container > img {
  width: 120%;
}

.line {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 75px;
  height: 2px;
  background-color: white;
  margin-top: 15px;
}

.item0 {
  grid-area: aside;
}
.item1 {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #2498eb;

  grid-area: nw;
}
.item2 {
  grid-area: ne;
}
.item3 {
  grid-area: sw;
}
.item4 {
  grid-area: se;
}

@media only screen and (max-width: 1230px) {
  .img-container > img {
    width: 100%;
  }

  .grid-container {
    width: 600px;
    grid-template-areas:
      "aside nw"
      "aside sw"
      "ne se";
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
  }
}

@media only screen and (max-width: 620px) {
  .grid-container {
    width: 100%;
    height: 100%;
    grid-template-areas:
      "aside"
      "aside"
      "ne"
      "nw"
      "sw"
      "se";
    grid-template-columns: 1fr;
    grid-template-rows: 2fr 1fr 1fr 1fr 1fr 1fr;
  }

  .item0 > img {
    height: 100%;
    width: 167%;
  }

  img {
    height: 100%;
  }
}
</style>
