<template scoped>
    <div class="speedometer-container">
        <div class="speedometer-text">
            <div class="static">Speed</div>
            <div class="dynamic">
                <span class="km">0</span>
                <span class="unit">KM/H</span>
            </div>
        </div>
        <div class="center-point"></div>
        <div class="speedometer-center-hide"></div>
        <div class="speedometer-bottom-hide"></div>
        <div class="arrow-container">
            <div class="arrow-wrapper arrow-angle-speedometer">
                <div class="arrow"></div>
            </div>
        </div>
        <div class="speedometer-scale speedometer-scale-1 "></div>
        <div class="speedometer-scale speedometer-scale-2"></div>
        <div class="speedometer-scale speedometer-scale-3"></div>
        <div class="speedometer-scale speedometer-scale-4"></div>
        <div class="speedometer-scale speedometer-scale-5"></div>
        <div class="speedometer-scale speedometer-scale-6"></div>
        <div class="speedometer-scale speedometer-scale-7"></div>
        <div class="speedometer-scale speedometer-scale-8"></div>
        <div class="speedometer-scale speedometer-scale-9"></div>
        <div class="speedometer-scale speedometer-scale-10"></div>
        <div class="speedometer-scale speedometer-scale-11"></div>
        <div class="speedometer-scale speedometer-scale-12"></div>
        <div class="speedometer-scale speedometer-scale-13"></div>
        <div class="speedometer-scale speedometer-scale-14"></div>
        <div class="speedometer-scale speedometer-scale-15"></div>
        <div class="speedometer-scale speedometer-scale-16"></div>
        <div class="speedometer-scale speedometer-scale-17"></div>
        <div class="speedometer-scale speedometer-scale-18"></div>
        <div class="speedometer-scale speedometer-scale-19"></div>
    </div>
</template>

<script scoped>
import $ from 'jquery';

export default {
  name: 'TheSpeedometer.vue',
  data() {
    return {
      speedometerScale: 19,
      maxSpeed: 36,
      speed: 0,
      currentScale: 1
    };
  },
  created() {
    this.getSpeed();
  },
  methods: {
    changeTextSpeed() {
      $('.km').text(this.speed);
    },
    calculateArrowAngleSpeed() {
      const proportion = this.speed / this.maxSpeed;
      const angle = proportion * 180;
      return angle;
    },
    changeArrowAngleSpeed() {
      const angle = this.calculateArrowAngleSpeed();
      $('.arrow-angle-speedometer').css({ transform: `rotate(${angle}deg)` });
    },
    changeActiveSpeed() {
      const proportion = this.speed / this.maxSpeed;
      this.currentScale = parseInt(proportion * this.speedometerScale);

      const activeScales = $('.speedometer-scale').slice(0, this.currentScale);
      let i = 1;
      activeScales.each(function () {
        $(this).addClass(`active-scale-${i}`);
        i++;
      });

      const inactiveScales = $('.speedometer-scale').slice(this.currentScale, this.maxSpeed + 2);
      i = this.currentScale + 1;
      inactiveScales.each(function () {
        $(this).removeClass(`active-scale-${i}`);
        i++;
      });
    },
    getSpeed() {
      // Use a função setInterval para atualizar a velocidade a cada 500 milissegundos
      const self = this;
      setInterval(() => {
        $.ajax({
            url : '../php/db_query_encoder.php',
            type : 'POST',
            success : function (result) {
              self.speed = result;
              self.changeTextSpeed();
              self.changeArrowAngleSpeed();
              self.changeActiveSpeed();
            },
          });
      }, 500);
    }
  },
};
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.speedometer-container {
    width: 300px;
    height: 300px;
    border: 3px solid black;
    border-radius: 50%;
    margin: 50px auto;
    position: relative;
}

.center-point {
    width: 20px;
    height: 20px;
    background-color: black;
    border-radius: 50%;
    position: absolute;
    top: 137px;
    left: 137px;
    z-index: 10;
}

.speedometer-scale {
    width: 8px;
    height: 280px;
    background-color: black;
    position: absolute;
    left: 143px;
    top: 7px;
}

.speedometer-scale-1 {
    transform: rotate(-90deg);
}

.speedometer-scale-2 {
    transform: rotate(-80deg);
}

.speedometer-scale-3 {
    transform: rotate(-70deg);
}

.speedometer-scale-4 {
    transform: rotate(-60deg);
}

.speedometer-scale-5 {
    transform: rotate(-50deg);
}

.speedometer-scale-6 {
    transform: rotate(-40deg);
}

.speedometer-scale-7 {
    transform: rotate(-30deg);
}

.speedometer-scale-8 {
    transform: rotate(-20deg);
}

.speedometer-scale-9 {
    transform: rotate(-10deg);
}

.speedometer-scale-10 {
    transform: rotate(0deg);
}

.speedometer-scale-11 {
    transform: rotate(10deg);
}

.speedometer-scale-12 {
    transform: rotate(20deg);
}

.speedometer-scale-13 {
    transform: rotate(30deg);
}

.speedometer-scale-14 {
    transform: rotate(40deg);
}

.speedometer-scale-15 {
    transform: rotate(50deg);
}

.speedometer-scale-16 {
    transform: rotate(60deg);
}

.speedometer-scale-17 {
    transform: rotate(70deg);
}

.speedometer-scale-18 {
    transform: rotate(80deg);
}

.speedometer-scale-19 {
    transform: rotate(90deg);
    height: 244px;
    top: 25px;
    left: 161px;
}

.active-scale-1 {
    background-color: green;
}

.active-scale-2 {
    background-color: rgb(8, 181, 8);
}

.active-scale-3 {
    background-color: rgb(21, 202, 21);
}

.active-scale-4 {
    background-color: rgb(43, 244, 43);
}

.active-scale-5 {
    background-color: rgb(79, 251, 79);
}

.active-scale-6 {
    background-color: rgb(133, 251, 79);
}

.active-scale-7 {
    background-color: rgb(199, 251, 79);
}

.active-scale-8 {
    background-color: rgb(228, 251, 79);
}

.active-scale-9 {
    background-color: rgb(251, 251, 79);
}

.active-scale-10 {
    background-color: rgb(251, 234, 79);
}

.active-scale-11 {
    background-color: rgb(251, 205, 79);
}

.active-scale-12 {
    background-color: rgb(251, 168, 79);
}

.active-scale-13 {
    background-color: rgb(251, 139, 79);
}

.active-scale-14 {
    background-color: rgb(251, 122, 79);
}

.active-scale-15 {
    background-color: rgb(251, 99, 79);
}

.active-scale-16 {
    background-color: rgb(251, 90, 79);
}

.active-scale-17 {
    background-color: rgb(247, 61, 47);
}

.active-scale-18 {
    background-color: rgb(247, 47, 47);
}

.active-scale-19 {
    background-color: red;
}

.speedometer-center-hide {
    width: 250px;
    height: 250px;
    background-color: white;
    border-radius: 50%;
    position: absolute;
    top: 22px;
    left: 22px;
    z-index: 9;
}

.speedometer-bottom-hide {
    width: 320px;
    height: 250px;
    background-color: white;
    position: absolute;
    z-index: 11;
    top: 160px;
    left: -14px;
    border-top: 1px solid;
}

.arrow-container {
    width: 160px;
    height: 160px;
    background-color: transparent;
    position: absolute;
    z-index: 12;
    top: 67px;
    left: 67px;
}

.arrow-wrapper {
    width: 160px;
    height: 160px;
    background-color: transparent;
    position: relative;
    transition: all 0.4s;
}

.arrow {
    width: 110px;
    height: 4px;
    background-color: purple;
    position: absolute;
    top: 78px;
    left: -30px;
}

.arrow-angle-speedometer {
    transform: rotate(0deg);
}

.speedometer-text {
    width: 180px;
    position: absolute;
    z-index: 20;
    left: 58px;
    top: 60px;
    text-align: center;
    font-weight: bold;
}

.static {
    font-size: 18px;
}

.dynamic {
    margin-top: 10px;
}

.km {
    font-size: 32px;
}

.unit {
    font-size: 14px;
    margin-left: 5px;
}</style>