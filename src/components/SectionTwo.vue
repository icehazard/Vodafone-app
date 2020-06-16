<template>
  <div>
    <div class="our-services">
      <span>{{ data.title }}</span>
    </div>
    <div class="d-flex justify-content-center align-items-center" id="section-two-container">
      <div class="card-section">
        <div class="card-title mb-70">{{ data.graphText }}</div>
        <div v-for="(item, idx) in data.stats" :key="item.idx" class="percentage-card">
          <div v-if="data.stats" class="d-flex justify-content-between">
            <div>{{ item.title.toUpperCase() }}</div>
            <div :id="['item' + idx]">{{ item.amount / 10 }}%</div>
          </div>
          <input type="range" min="0" max="1000" :value="item.amount" class="slider" :id="['range' + idx]" />
        </div>
      </div>
      <div class="card-section validate">
        <div class="card-title">{{ data.formText }}</div>
        <div class="card-subtitle">
          {{ data.graphText }}
        </div>

        <form v-if="data.formLabels" class="center">
          <div class="form-group">
            <input
              type="tel"
              data-validation="length number custom required"
              data-validation-regexp="^(2|6|0|\+)"
              data-validation-length="10"
              class="form-control"
              id="phone"
              :placeholder="data.formLabels[0]"
            />
          </div>
          <div class="form-group">
            <input type="text" name="email" data-validation="email required" class="form-control" id="email" :placeholder="data.formLabels[1]" />
          </div>
          <div class="form-group error">
            <input
              type="password"
              data-validation="strength custom required"
              data-validation-strength="3"
              data-validation-regexp="^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$"
              class="form-control"
              id="password"
              :placeholder="data.formLabels[2]"
            />
          </div>
          <div class="center">
            <button type="button" @click="validateForm()" value="Validate" class="btn btn-primary submit-button">
              {{ data.buttonText }}
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["data"],
  methods: {
    initSliders() {
      function addListener(n) {
        let s1 = document.createElement("style");
        document.querySelector("[id=range" + n + "]").appendChild(s1);
        let r1 = document.querySelector("[id=range" + n + "]");
        r1.addEventListener(
          "input",
          function() {
            let value = Math.round(this.value / 10) + "%";
            document.getElementById("item" + n).innerHTML = value;
            var val = value + "100%";
            s1.textContent =
              ".js input[id=range" +
              n +
              "]::-webkit-slider-runnable-track{background-size:" +
              val +
              "}" +
              ".js input[id=range" +
              n +
              "]::-moz-range-track{background-size:" +
              val +
              "}";
            s1.textContent += ".js input[id=range" + n + '] /deep/ #thumb:before{content:"' + this.value + '%"}';
          },
          false
        );
      }
      for (let x in this.data.stats) {
        addListener(x);
      }
    },
    validateForm() {
      var errors = [];
      $.validate({
        modules: "security",
        onElementValidate: function(valid, $el, $form, errorMess) {
          let input = $("#phone")[0].value;
          let length = $("#phone")[0].attributes["data-validation-length"].textContent;

          if (input[0] == "+") {
            $("#phone")[0].attributes["data-validation-length"].textContent = 13;
          } else if (input[0] == "0") {
            $("#phone")[0].attributes["data-validation-length"].textContent = 14;
          } else {
            $("#phone")[0].attributes["data-validation-length"].textContent = 10;
          }
        },
      });
    },
  },
  mounted() {
    this.initSliders();
  },
};
</script>

<style>
.our-services {
  display: flex;
  align-items: flex-end;
  color: #1292ee;
  padding-bottom: 22px;
}

.card-subtitle {
  max-width: 466px;
  text-align: center;
  font-size: 14px;
  color: #748494;
  transform: translateY(-50%);
}

.validate {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.submit-button {
  width: 160px;
  height: 52px;
  background-color: #166dd5;
  border-radius: 2px;
  font-family: "MyriadPro";
  font-size: 15px;
}

.form-control {
  background-color: #f5f5f5;
  border: 0;
  width: 370px;
  height: 54px;
  margin-top: 8px;
}

form {
  margin-top: 45px;
}

.card-section {
  height: 711px;
  width: 587px;
}

.card-title {
  font-size: 32px;
  height: 81px;
}

.slider {
  -webkit-appearance: none;
  width: 100%;
  height: 5px;
  border-radius: 5px;
  background: #f5f7fd;
  outline: none;
  opacity: 0.7;
  -webkit-transition: 2s;
  transition: opacity 2s;
}

.percentage-card {
  height: 80px;
}

@media only screen and (max-width: 420px) {
  .form-control {
    width: 360px;
  }
}

@media only screen and (max-width: 400px) {
  .form-control {
    width: 330px;
  }
}

@media only screen and (max-width: 380px) {
  .form-control {
    width: 270px;
  }
}

input[type="range"]::-webkit-slider-runnable-track {
  background-repeat: no-repeat;
  height: 5px;
}

input[type="range"]::-moz-range-track {
  background-repeat: no-repeat;
  height: 5px;
}

input[id="range0"]::-webkit-slider-runnable-track {
  background-image: linear-gradient(90deg, rgb(0, 139, 190), rgb(88, 254, 238));
  background-size: 60% 100%;
}

input[id="range0"]::-moz-range-track {
  background-image: linear-gradient(90deg, rgb(0, 139, 190), rgb(88, 254, 238));
  background-size: 60% 100%;
}

input[id="range1"]::-webkit-slider-runnable-track {
  background-image: linear-gradient(90deg, #2e77ac, #73bff6);
  background-size: 30% 100%;
}

input[id="range1"]::-moz-range-track {
  background-image: linear-gradient(90deg, #2e77ac, #73bff6);
  background-size: 30% 100%;
}

input[id="range2"]::-webkit-slider-runnable-track {
  background-image: linear-gradient(90deg, #eb8459, #fabcaf);
  background-size: 30% 100%;
}

input[id="range2"]::-moz-range-track {
  background-image: linear-gradient(90deg, #eb8459, #fabcaf);
  background-size: 30% 100%;
}

input[id="range3"]::-webkit-slider-runnable-track {
  background-image: linear-gradient(90deg, #7d55d9, #f9aada);
  background-size: 80% 100%;
}

input[id="range3"]::-moz-range-track {
  background-image: linear-gradient(90deg, #7d55d9, #f9aada);
  background-size: 80% 100%;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 23px;
  height: 24px;
  border: 0;
  background-repeat: no-repeat;
  cursor: pointer;
  transform: translateY(-35%);
}

input[type="range"]::-moz-range-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 23px;
  height: 24px;
  border: 0;
  background-repeat: no-repeat;
  cursor: pointer;
}

input[id="range0"]::-webkit-slider-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/one_hteuuq.png");
}

input[id="range0"]::-moz-range-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/one_hteuuq.png");
}

input[id="range1"]::-webkit-slider-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/two_ilka2h.png");
}

input[id="range1"]::-moz-range-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/two_ilka2h.png");
}

input[id="range2"]::-webkit-slider-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/three_b2pjtv.png");
}

input[id="range2"]::-moz-range-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/three_b2pjtv.png");
}

input[id="range3"]::-webkit-slider-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/four_zmh3oz.png");
}

input[id="range3"]::-moz-range-thumb {
  background: url("https://res.cloudinary.com/dorhsrqla/image/upload/v1592249309/four_zmh3oz.png");
}
</style>
