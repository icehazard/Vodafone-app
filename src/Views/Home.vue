<template>
  <div>
    <Header />
    <div class="body">
      <div class="body-container">
        <div class="banner">
          <div class="banner-top">
            <h1 class="section-text ">{{ home.description }}</h1>
          </div>
          <div class="section_container">
            <button class="section-controller" @click="sectionIndex = 0">
              <span>Section 1</span>
              <span v-show="sectionIndex == 0" class="dot"></span>
            </button>
            <button class="section-controller" @click="sectionIndex = 1">
              <span>Section 2</span>
              <span v-show="sectionIndex == 1" class="dot"></span>
            </button>
          </div>
        </div>
        <SectionOne v-if="sectionIndex == 0" :data="data" />
        <SectionTwo v-if="sectionIndex == 1" :data="sectionTwo" />
      </div>
    </div>
  </div>
</template>

<script>
import Header from "../components/Header";
import SectionOne from "../components/SectionOne";
import SectionTwo from "../components/SectionTwo";

export default {
  name: "Home",
  components: {
    Header,
    SectionOne,
    SectionTwo,
  },
  data() {
    return {
      sectionIndex: 0,
      data: [],
      sectionTwo: [],
      home: [],
    };
  },
  methods: {
    async getHomeData() {
      let response = await fetch(`https://voda-react-assessment.herokuapp.com/home`);
      let data = await response.json();
      this.data = data[0].sections[0].images;
      this.sectionTwo = data[0].sections[1];
      this.home = data[0];
    },
  },
  mounted() {
    this.getHomeData();
  },
};
</script>

<style lang="less">
@font-face {
  font-family: "MyriadPro";
  src: url("https://res.cloudinary.com/dorhsrqla/raw/upload/v1592299894/MyriadPro-Regular_hvv9ja.otf");
}

.section_container {
  display: flex;
  justify-content: flex-end;
  margin-top: 25px;
}

.banner {
  height: 260px;
}

.section-text {
  margin: 0;
}

.dot {
  height: 10px;
  width: 10px;
  background-color: #1292ee;
  border-radius: 50%;
  display: inline-block;
  margin-top: 10px;
}

.section-controller {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 14px;
  margin-left: 20px;
  border: none;
  background-color: rgba(0, 139, 139, 0);
}

.banner-top {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  height: 100px;
}

.body {
  display: flex;
  justify-content: center;
}
.body-container {
  width: 1170px;
}

body {
  font-family: "MyriadPro";
}

@media only screen and (max-width: 1230px) {
  .body-container {
    width: 600px;
  }

  .card-section {
    height: 570px;
  }

  #section-two-container {
    flex-direction: column;
  }

  .banner {
    height: auto;
  }

  .our-services {
    margin-left: 6px;
  }
}

@media only screen and (max-width: 620px) {
  .our-services {
    margin-left: 0px;
  }

  .body-container {
    width: 100%;
    height: auto;
  }

  .body {
    padding: 0 15px 0 15px;
    display: block;
  }

  .card-section {
    width: 100%;
  }

  .card-title {
    font-size: 24px;
  }
}
</style>
