<template scoped>
<div class="wattmeter-container">
    <div class="wattmeter-text">
        <div class="static">Power</div>
        <div class="dynamic">
            <span class="watts">0</span>
            <span class="unit">W</span>
        </div>
    </div>
    <div class="center-point"></div>
    <div class="wattmeter-center-hide"></div>
    <div class="wattmeter-bottom-hide"></div>
    <div class="arrow-container">
        <div class="arrow-wrapper arrow-angle-wattmeter">
            <div class="arrow"></div>
        </div>
    </div>
    <div class="wattmeter-scale wattmeter-scale-1 "></div>
    <div class="wattmeter-scale wattmeter-scale-2"></div>
    <div class="wattmeter-scale wattmeter-scale-3"></div>
    <div class="wattmeter-scale wattmeter-scale-4"></div>
    <div class="wattmeter-scale wattmeter-scale-5"></div>
    <div class="wattmeter-scale wattmeter-scale-6"></div>
    <div class="wattmeter-scale wattmeter-scale-7"></div>
    <div class="wattmeter-scale wattmeter-scale-8"></div>
    <div class="wattmeter-scale wattmeter-scale-9"></div>
    <div class="wattmeter-scale wattmeter-scale-10"></div>
    <div class="wattmeter-scale wattmeter-scale-11"></div>
    <div class="wattmeter-scale wattmeter-scale-12"></div>
    <div class="wattmeter-scale wattmeter-scale-13"></div>
    <div class="wattmeter-scale wattmeter-scale-14"></div>
    <div class="wattmeter-scale wattmeter-scale-15"></div>
    <div class="wattmeter-scale wattmeter-scale-16"></div>
    <div class="wattmeter-scale wattmeter-scale-17"></div>
    <div class="wattmeter-scale wattmeter-scale-18"></div>
    <div class="wattmeter-scale wattmeter-scale-19"></div>
</div>
</template>

<script scoped>
import $ from 'jquery';

export default {
  name: 'TheWattmeter.vue',
  data() {
    return {
      wattmeterScale: 19,
      maxPower: 400,
      power: 0,
      currentScale: 1
    };
  },
  created() {
    this.getPower();
  },
  methods: {
    changeTextPower() {
      $('.watts').text(this.power);
    },
    calculateArrowAnglePower() {
      const proportion = this.power / this.maxPower;
      const angle = proportion * 180;
      return angle;
    },
    changeArrowAnglePower() {
      const angle = this.calculateArrowAnglePower();
      $('.arrow-angle-wattmeter').css({ transform: `rotate(${angle}deg)` });
    },
    changeActivePower() {
      const proportion = this.power / this.maxPower;
      this.currentScale = parseInt(proportion * this.wattmeterScale);

      const activeScales = $('.wattmeter-scale').slice(0, this.currentScale);
      activeScales.each(function () {
        $(this).addClass(`active-scale`);
      });

      const inactiveScales = $('.wattmeter-scale').slice(this.currentScale, this.wattmeterScale + 2);
      inactiveScales.each(function () {
        $(this).removeClass(`active-scale`);
      });
    },
    getPower() {
      // Use a função setInterval para atualizar a potencia a cada intervalo
      const self = this;
      setInterval(() => {
        $.ajax({
            url : '../php/db_query_ina226.php',
            type : 'POST',
            dataType: 'json',
            success : function (result) {
              self.power = result.power;
              self.changeTextPower();
              self.changeArrowAnglePower();
              self.changeActivePower();
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

.wattmeter-container {
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

.wattmeter-scale {
    width: 8px;
    height: 280px;
    background-color: black;
    position: absolute;
    left: 143px;
    top: 7px;    
}

.wattmeter-scale-1 {
    transform: rotate(-90deg);
}
.wattmeter-scale-2 {
    transform: rotate(-80deg);
}
.wattmeter-scale-3 {
    transform: rotate(-70deg);
}
.wattmeter-scale-4 {
    transform: rotate(-60deg);
}
.wattmeter-scale-5 {
    transform: rotate(-50deg);
}
.wattmeter-scale-6 {
    transform: rotate(-40deg);
}
.wattmeter-scale-7 {
    transform: rotate(-30deg);
}
.wattmeter-scale-8 {
    transform: rotate(-20deg);
}
.wattmeter-scale-9 {
    transform: rotate(-10deg);
}
.wattmeter-scale-10 {
    transform: rotate(0deg);
}
.wattmeter-scale-11 {
    transform: rotate(10deg);
}
.wattmeter-scale-12 {
    transform: rotate(20deg);
}
.wattmeter-scale-13 {
    transform: rotate(30deg);
}
.wattmeter-scale-14 {
    transform: rotate(40deg);
}
.wattmeter-scale-15 {
    transform: rotate(50deg);
}
.wattmeter-scale-16 {
    transform: rotate(60deg);
}
.wattmeter-scale-17 {
    transform: rotate(70deg);
}
.wattmeter-scale-18 {
    transform: rotate(80deg);
}
.wattmeter-scale-19 {
    transform: rotate(90deg);
    height: 244px;
    top: 25px;
    left: 161px;
}

.active-scale {
    background-color: purple;
}

.wattmeter-center-hide {
    width: 250px;
    height: 250px;
    background-color: white;
    border-radius: 50%;
    position: absolute;
    top: 22px;
    left: 22px;
    z-index: 9;
}

.wattmeter-bottom-hide {
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

.arrow-angle-wattmeter {
    transform: rotate(0deg);
}

.wattmeter-text {
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

.watts {
    font-size: 32px;
}

.unit {
    font-size: 14px;
    margin-left: 5px;
}
</style>