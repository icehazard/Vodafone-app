<template>
  <div class="section-two" id="section-two-container">
    <div class="card-section">
      <div class="card-title mb-70">We create websites and campaigns that expose new opportunities</div>
      <div class="percentage-card">
        <div class="d-flex justify-content-between">
          <div>PERCENTAGE 1</div>
          <div id="percentageDisplayOne">60%</div>
        </div>
        <input type="range" min="0" max="100" value="60" class="slider" id="rangeOne" />
      </div>
      <div class="percentage-card">
        <div class="d-flex justify-content-between">
          <div>PERCENTAGE 2</div>
          <div id="percentageDisplayTwo">20%</div>
        </div>
        <input type="range" min="0" max="100" value="20" class="slider" id="rangeTwo" />
      </div>
      <div class="percentage-card">
        <div class="d-flex justify-content-between">
          <div>PERCENTAGE 3</div>
          <div id="percentageDisplayThree">5%</div>
        </div>
        <input type="range" min="0" max="100" value="5" class="slider" id="rangeThree" />
      </div>
      <div class="percentage-card">
        <div class="d-flex justify-content-between">
          <div>PERCENTAGE 4</div>
          <div id="percentageDisplayFour">25%</div>
        </div>
        <input type="range" min="0" max="100" value="25" class="slider" id="rangeFour" />
      </div>
    </div>
    <div class="card-section validate">
      <div class="card-title">Validate your info</div>
      <div
        class="card-subtitle"
      >We work with ecosystem leaders, corporations and startups worldwide. How can we help you?</div>
      <form class="center">
        <div class="form-group">
          <input
            type="tel"
            data-validation="length custom"
            data-validation-regexp="^(2|6|0|\+)"
            data-validation-length="10"
            class="form-control"
            id="phone"
            placeholder="Your Phone"
          />
        </div>
        <div class="form-group">
          <input
            type="text"
            name="email"
            data-validation="email"
            class="form-control"
            id="email"
            placeholder="Your Email"
          />
        </div>
        <div class="form-group error">
          <input
            type="password"
            data-validation="strength"
            data-validation-strength="1"
            class="form-control"
            id="password"
            placeholder="Password"
          />
        </div>
        <div class="center">
          <button
            type="button"
            @click="validateForm()"
            value="Validate"
            class="btn btn-primary submit-button font-weight-lighter"
          >Submit</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: ["data"],
  name: "Home",
  components: {},
  data() {
    return {};
  },
  methods: {
    async getHomeData() {
      let response = await fetch(
        `https://voda-react-assessment.herokuapp.com/home`
      );
      this.data = await response.json();
      console.log("getHomeData -> this.data ", this.data);
    },

    initSliders() {
      const s1 = document.createElement("style"),
        s2 = document.createElement("style"),
        s3 = document.createElement("style"),
        s4 = document.createElement("style"),
        r1 = document.querySelector("[id=rangeOne]"),
        r2 = document.querySelector("[id=rangeTwo]"),
        r3 = document.querySelector("[id=rangeThree]"),
        r4 = document.querySelector("[id=rangeFour]");

      document.body.appendChild(s1);
      document.body.appendChild(s2);
      document.body.appendChild(s3);
      document.body.appendChild(s4);

      r1.addEventListener(
        "input",
        function() {
          document.getElementById("percentageDisplayOne").innerHTML =
            this.value + "%";
          var val = this.value + "% 100%";
          s1.textContent =
            ".js input[id=rangeOne]::-webkit-slider-runnable-track{background-size:" +
            val +
            "}" +
            ".js input[id=rangeOne]::-moz-range-track{background-size:" +
            val +
            "}";
          s1.textContent +=
            '.js input[id=rangeOne] /deep/ #thumb:before{content:"' +
            this.value +
            '%"}';
        },
        false
      );

      r2.addEventListener(
        "input",
        function() {
          document.getElementById("percentageDisplayTwo").innerHTML =
            this.value + "%";
          var val = this.value + "% 100%";
          s2.textContent =
            ".js input[id=rangeTwo]::-webkit-slider-runnable-track{background-size:" +
            val +
            "}" +
            ".js input[id=rangeTwo]::-moz-range-track{background-size:" +
            val +
            "}";
          s2.textContent +=
            '.js input[id=rangeTwo] /deep/ #thumb:before{content:"' +
            this.value +
            '%"}';
        },
        false
      );

      r3.addEventListener(
        "input",
        function() {
          document.getElementById("percentageDisplayThree").innerHTML =
            this.value + "%";
          var val = this.value + "% 100%";
          s3.textContent =
            ".js input[id=rangeThree]::-webkit-slider-runnable-track{background-size:" +
            val +
            "}" +
            ".js input[id=rangeThree]::-moz-range-track{background-size:" +
            val +
            "}";
          s3.textContent +=
            '.js input[id=rangeThree] /deep/ #thumb:before{content:"' +
            this.value +
            '%"}';
        },
        false
      );

      r4.addEventListener(
        "input",
        function() {
          document.getElementById("percentageDisplayFour").innerHTML =
            this.value + "%";
          var val = this.value + "% 100%";
          s4.textContent =
            ".js input[id=rangeFour]::-webkit-slider-runnable-track{background-size:" +
            val +
            "}" +
            ".js input[id=rangeFour]::-moz-range-track{background-size:" +
            val +
            "}";
          s4.textContent +=
            '.js input[id=rangeFour] /deep/ #thumb:before{content:"' +
            this.value +
            '%"}';
        },
        false
      );
    },
    validateForm() {
      var errors = [];
      $.validate({
        modules: "security",
        onElementValidate: function(valid, $el, $form, errorMess) {
          let input = $("#phone")[0].value;
          let length = $("#phone")[0].attributes["data-validation-length"]
            .textContent;

          if (input[0] == "+") {
            $("#phone")[0].attributes[
              "data-validation-length"
            ].textContent = 13;
          } else if (input[0] == "0") {
            $("#phone")[0].attributes[
              "data-validation-length"
            ].textContent = 14;
          } else {
            $("#phone")[0].attributes[
              "data-validation-length"
            ].textContent = 10;
          }
        }
      });
    }
  },
  mounted() {
    this.validateForm();
    this.initSliders();
  }
};
</script>


<style>
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

input[id="rangeOne"]::-webkit-slider-runnable-track {
  /* only Firefox & Chrome/ Opera */
  background-image: linear-gradient(90deg, rgb(0, 139, 190), rgb(88, 254, 238));
  background-repeat: no-repeat;
  background-size: 60% 100%;
  height: 5px;
}

input[id="rangeTwo"]::-webkit-slider-runnable-track {
  /* only Firefox & Chrome/ Opera */
  background-image: linear-gradient(90deg, #2e77ac, #73bff6);
  background-repeat: no-repeat;
  background-size: 20% 100%;
  height: 5px;
}

input[id="rangeThree"]::-webkit-slider-runnable-track {
  /* only Firefox & Chrome/ Opera */
  background-image: linear-gradient(90deg, #eb8459, #fabcaf);
  background-repeat: no-repeat;
  background-size: 5% 100%;
  height: 5px;
}

input[id="rangeFour"]::-webkit-slider-runnable-track {
  /* only Firefox & Chrome/ Opera */
  background-image: linear-gradient(90deg, #7d55d9, #f9aada);
  background-repeat: no-repeat;
  background-size: 25% 100%;
  height: 5px;
}

input[id="rangeOne"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 23px;
  height: 24px;
  border: 0;
  background: url("/imgs/one.png");
  background-repeat: no-repeat;
  cursor: pointer;
  transform: translateY(-35%);
}

input[id="rangeTwo"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 23px;
  height: 24px;
  border: 0;
  background: url("/imgs/two.png");
  background-repeat: no-repeat;
  cursor: pointer;
  transform: translateY(-35%);
}

input[id="rangeThree"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 23px;
  height: 24px;
  border: 0;
  background: url("/imgs/three.png");
  background-repeat: no-repeat;
  cursor: pointer;
  transform: translateY(-35%);
}

input[id="rangeFour"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 23px;
  height: 24px;
  border: 0;
  background: url("/imgs/four.png");
  background-repeat: no-repeat;
  cursor: pointer;
  transform: translateY(-35%);
}
</style>