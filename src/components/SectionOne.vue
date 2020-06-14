<template>
  <div class="section-one grid-container">
    <div v-if="data[0]" id="item1" class="item1 img-container">
      <img class="rectangle" :src="data[0].img" :alt="data[0].title" />
    </div>
    <div v-if="data[1]" id="item2" class="img-container">
      <img v-if="data[1]" :src="data[1].img" :alt="data[1].title" />
      <div v-else class="center">
        <i class="fa fa-eye curser-p" aria-hidden="true"></i>
        <div>{{data[1].title}}</div>
        <div class="line"></div>
      </div>
    </div>
    <div v-if="data[2]" class="item3 img-container">
      <img :src="data[2].img" :alt="data[2].title" />
    </div>
    <div v-if="data[3]" class="item4 img-container">
      <img :src="data[3].img" :alt="data[3].title" />
    </div>
    <div v-if="data[4]" class="item5 img-container">
      <img :src="data[4].img" :alt="data[4].title" />
    </div>
  </div>
</template>

<script>
export default {
  props: ["data"],
};
</script>

<style>
.img-container > img {
  width: 120%;
}

.grid-container > div {
  background-color: #cccccc;
  text-align: center;
  padding: 0;
  font-size: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  position: relative;
  overflow: hidden;
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

.item1 {
  grid-area: aside;
}

#item2 {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #2498eb;
  color: white;
  grid-area: nw;
}

.item3 {
  grid-area: ne;
}

.item4 {
  grid-area: sw;
}

.item5 {
  grid-area: se;
}

.grid-container {
  width: 1170px;
  height: 630px;
  margin-bottom: 136px;
  display: grid;
  grid-template-areas:
    "aside nw ne "
    "aside sw se ";

  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  grid-gap: 30px;
  padding: 10px;
}

.percentage-card {
  height: 80px;
}

.mb-70 {
  margin-bottom: 70px;
}

@media only screen and (max-width: 1230px) {
  .img-container > img {
    width: 101%;
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
    height: 60%;
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
  img.rectangle {
    height: 100%;
    width: 100%;
}
}
</style>
