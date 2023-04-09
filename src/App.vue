<template>
<body>
<header>EQUIPE MILHAGEM</header>
<div class="dashboard">
    <div class="area-1">
        <div class="termometro">
            <TheTermometer />
        </div>
        <div class="velocimetro">
            <TheSpeedometer />
        </div>
    </div>
    <div class="area-tensao-corrente">
        <div class="tensao-corrente">
            <TheDisplay />
        </div>
        <div class="graficos">
            <div class="chart-voltage">

            </div>
            <div class="chart-current">

            </div>
        </div>
    </div>
    <div class='area-wattmetro'>
        <div class="dummy"></div>
        <div class="wattmetro">
            <TheWattmeter />
        </div>
    </div>
    <div class="area-mapa">MAPA</div>
</div>
</body>
</template>

<script>
    import TheWattmeter from './components/TheWattmeter.vue';
    import TheSpeedometer from './components/TheSpeedometer.vue';
    import TheTermometer from './components/TheTermometer.vue';
    import TheDisplay from './components/TheDisplay.vue';

    export default {
        name: 'App',
        components: {
            TheWattmeter,
            TheSpeedometer,
            TheTermometer,
            TheDisplay
        }
    }
</script>

<style>
@import './css/reset.css';
header {
    height: 50px;
    background-color: #155c94;
}

.dashboard {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-auto-rows: 310px;
}

.area-1 {
    display: grid;
    grid-template-columns: 20% 80%;
    z-index: 1;
}

.termometro {
    height: 100vh;
    margin: 0;
    font-family: "Jaldi", sans-serif;
    font-size: 14px;
    color: white;
}

.area-tensao-corrente {
    display: grid;
    grid-template-rows: 20% 80%;
}

.graficos {
    display: grid;
    grid-template-columns: 1fr 1fr;
}

.chart-voltage {
    background-color: red;
}

.chart-current {
    background-color: rgb(99, 0, 0);
}

.area-wattmetro {
    display: grid;
    grid-template-columns: 20% 80%;
    z-index: 10;
}

.area-mapa {
    background-color: yellow;
}
</style>
