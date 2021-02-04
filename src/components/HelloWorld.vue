<template>
  <div class="mainDiv">
    <div class="container" :class="backgroundVariable + '_' + chosenShape">
      <p
        class="text"
        :style="{
          top: top + '%',
          'font-size': fontsize + 'vw',
          left: left + '%',
          color: color,
        }"
      >
        {{ text }}
      </p>
    </div>
    <div class="menu">
      <button @click="stage = 1" class="w-64 rounded button reset">
        Start over
      </button>
      <div v-if="stage == 1" class="bged2">
        <!--         <select name="" id="" >
        <option @click="backgroundVariable = 'gray'">Grey</option>
        <option @click="backgroundVariable = 'wood'">Wood</option>
        </select> -->
        <button class="button material" @click="backgroundVariable = 'gray'">
          Gray
        </button>
        <button class="button material" @click="backgroundVariable = 'wood'">
          Wood
        </button>
        <br />
        <button @click="(stage = 2), availBG()">NEXT</button>
      </div>

      <div v-if="stage == 2">
        <span v-for="(shape, index) in allowedShapes" v-bind:key="index">
          <img
            class="shape"
            @click="chosenShape = shape"
            v-bind:class="shape"
          />
        </span>

        <br />
        <button @click="stage = 3">NEXT</button>
      </div>
      <div v-if="stage == 3">
        Text:
        <input type="text" v-model="text" class="texted" />
        FOnt size
        <input type="text" v-model="fontsize" /><br />
        Top:
        <input type="number" v-model="top" />
        <button @click="topup">Top up</button>
        <button @click="topdown">Top down</button>
        Left:
        <input type="text" v-model="left" />
        <button @click="leftup">Left</button>
        <button @click="leftdown">Right</button>
        <br />
        COLOR (HEX) :
        <input
          style="width: 300px; margin: 10px 0"
          type="text"
          v-model="color"
        />
        <br />
        <div v-if="backgroundVariable === 'wood'">
          <button @click="color = '#000000'">BLACK</button>
          <button @click="color = '#FFFFFF'">WHITE</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      stage: 1,
      text: "Your text here",
      top: 50,
      left: 50,
      fontsize: 3,
      backgroundVariable: "wood",
      shapeVarialbe: "square",
      allowedShapes: ["rect"],
      chosenShape: "rect",
      color: "#FFFFFF",
    };
  },
  methods: {
    topup: function () {
      this.top -= 1;
      console.log(this.top);
    },
    leftup: function () {
      this.left -= 1;
      console.log("Left " + this.left);
    },
    topdown: function () {
      this.top += 1;
    },
    leftdown: function () {
      this.left += 1;
    },
    availBG: function () {
      if (this.backgroundVariable === "wood") {
        //this.$set(this.allowedShapes, 1, "square");
        this.allowedShapes = ["rect", "square", "thin_rect"];
      } else if (this.backgroundVariable === "gray") {
        //this.$set(this.allowedShapes, 1, "rect");
        this.allowedShapes = ["rect"];
      } else if (this.backgroundVariable === "acrylic") {
        //this.$set(this.allowedShapes, 1, "rect");
        this.allowedShapes = [
          "circle",
          "square",
          "rect",
          "thin_rect",
          "number",
        ];
      }
    },
    changeBack: function (background) {
      this.backgroundVariable = background;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mainDiv {
  background: url("https://mk0designahouse3b79p.kinstacdn.com/app/themes/dahs/assets/images/red_bg.jpg");
  color: white;
}
.container {
  width: 375px;
  margin: 0 auto;
  height: 300px;
  position: relative;
  overflow: hidden;
  padding-bottom: 25px;
}
.image {
  z-index: 1;
}
.text {
  top: 50%;
  left: 50%;
  position: absolute;
  z-index: 99999;
  color: white;
  transform: translate(-50%, -80%);
}
.menu {
  padding-top: 25px;
  background: white !important;
}
.button {
  background: #ededed;
  border: 0;
  padding: 5px 10px;
  font-size: 1em;
  margin: 5px 10px;
}
/* base bg */
.gray {
  background: url("https://www.designahousesign.com/app/themes/dahs/assets/sign-images/GR_engraved_8.png");
  background-repeat: no-repeat;
  background-position: center center;
}
.wood {
  background: url("https://www.designahousesign.com/app/themes/dahs/assets/sign-images/OA_8.png");
  background-repeat: no-repeat;
  background-position: center center;
}
/* material_shape images */
.gray_rect {
  background: url("https://www.designahousesign.com/app/themes/dahs/assets/sign-images/GR_engraved_8.png");
  background-repeat: no-repeat;
  background-position: center center;
}
.wood_rect {
  background: url("https://www.designahousesign.com/app/themes/dahs/assets/sign-images/OA_8.png");
  background-repeat: no-repeat;
  background-position: center center;
}
.wood_thin_rect {
  background: url("https://www.designahousesign.com/app/themes/dahs/assets/sign-images/OA_12.png");
  background-repeat: no-repeat;
  background-position: center center;
}
.wood_square {
  background: url("https://www.designahousesign.com/app/themes/dahs/assets/sign-images/OA_20.png");
  background-repeat: no-repeat;
  background-position: center center;
}
/* SHapes and types */
.shape {
  margin: 5px;
  background-size: cover !important;
  background-repeat: no-repeat !important;
  height: 75px;
  width: 75px;
  cursor: pointer;
  padding-top: 0px;
  margin-bottom: 10px;
  height: 50px;
  position: relative;
  background-size: 35%;
  border: 0px solid transparent !important;
  border-radius: 5px;
}
.square {
  background: url(https://www.designahousesign.com/app/themes/dahs/assets/images/20_sp.png) no-repeat;
}
.rect {
  background: url(https://www.designahousesign.com/app/themes/dahs/assets/images/08_sp.png) no-repeat !important;
}
.thin_rect {
  background: url(https://www.designahousesign.com/app/themes/dahs/assets/images/12_sp.png) no-repeat;
}

input {
  width: 20px;
  color: black !important;
}
input.texted {
  width: 150px;
  color: black !important;
}
div {
  color: black;
  font-weight: 560;
  font-size: 19px;
}
</style>
