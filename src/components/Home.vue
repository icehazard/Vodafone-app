<template>
  <div>
    <Header />
    <div class="body">
      <div class="body-container">
        <div class="banner">
          <div class="banner-top">
            <h1 class="section-text">{{data.description}}</h1>
          </div>
          <div class="section_container">
            <div class="section-controller" @click="setFrame(0)">
              <span>Section 1</span>
              <span class="dot"></span>
            </div>
            <div class="section-controller" @click="setFrame(1)">
              <span>Section 2</span>
              <span class="dot"></span>
            </div>
          </div>
          <div class="our-services section-two">
            <span>Our Services</span>
          </div>
        </div>
        <SectionOne :data="data" />
        <SectionTwo :data="data" />
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./Header";
import SectionOne from "./SectionOne";
import SectionTwo from "./SectionTwo";

export default {
  name: "Home",
  components: {
    Header,
    SectionOne,
    SectionTwo
  },
  data() {
    return {
      sectionIndex: 1,
      data: []
    };
  },
  methods: {
    setFrame(x) {
      let sectionOne = document.getElementsByClassName("section-one")[0];
      let sectionTwo = document.getElementsByClassName("section-two")[0];
      let sectionThree = document.getElementsByClassName("section-two")[1];
      if (x == 0) {
        sectionOne.style.display = "grid";
        sectionTwo.style.display = "none";
        sectionThree.style.display = "none";
      } else {
        sectionThree.style.display = "flex";
        sectionTwo.style.display = "flex";
        sectionOne.style.display = "none";
      }
      this.sectionButtons(x);
    },
    sectionButtons(n) {
      let dots = document.getElementsByClassName("dot");
      for (let i = 0; i < dots.length; i++) {
        dots[i].style.visibility = "hidden";
      }
      dots[n].style.visibility = "visible";
    },
    async getHomeData(){
      let response = await fetch(`https://voda-react-assessment.herokuapp.com/home`);
      let data = await response.json();
      this.data = data[0].sections[0].images
    }
  },
  mounted() {
    this.setFrame(0);
     this.getHomeData()
  }
};
</script>

<style lang="less">
@font-face {
  font-family: "MyriadPro";
  src: url("/fonts/MyriadPro-Regular.otf");
}

.container-toolbar > div {
  padding: 20px;
}

.section_container {
  display: flex;
  justify-content: flex-end;
}

.banner {
  height: 260px;
}

.center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}



.section-text {
  margin: 0;
  transform: translatey(50%);
}

.our-services {
  display: flex;
  align-items: flex-end;
  color: #1292ee;
  height: 80px;
  padding-bottom: 22px;
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
  justify-content: center;
  align-items: center;
  padding: 14px;
  margin-left: 20px;
  cursor: pointer;
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
  background-color: #f8faff;
  z-index: 4;
  position: relative;
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
}

@media only screen and (max-width: 620px) {


  .body-container {
    width: 100%;
  }

  .body {
    padding: 0 15px 0 15px;

    z-index: 4;
  }

  .card-section {
    width: 100%;
  }

  .card-title {
    height: auto;
    font-size: 24px;
  }
}
</style>
