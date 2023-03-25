<template>
<body>
<header>EQUIPE MILHAGEM</header>
<div class="dashboard">
    <div class="area-1">
        <div class="velocimetro">
            ENCODER
        </div>
        <div class="termometro">
            LM35
        </div>
    </div>
    <div class="area-tensao-corrente">
        <div class="tensao-corrente">
            9.05V / 4.41A
        </div>
        <div class="graficos">
            GRAFICOS
        </div>
    </div>
    <div class='area-wattmetro'>
        <TheWattmeter />
    </div>
    <div class="area-mapa">MAPA</div>
</div>
</body>
</template>

<script>
    import TheWattmeter from './components/TheWattmeter.vue';

    export default {
        name: 'App',
        components: {
            TheWattmeter
        }
    }
</script>

<style>
@import './css/reset.css';
header {
    height: 50px;
    background-color: aqua;
}

.dashboard {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-auto-rows: 310px;
}

.area-1 {
    background-color: blue;
    display: grid;
    grid-template-columns: 80% 20%;
}

.velocimetro {
    background-color: rgb(57, 57, 167) ;
}

.termometro {
    background-color: rgb(16, 16, 94);
}

.area-tensao-corrente {
    background-color: red;
    display: grid;
    grid-template-rows: 20% 80%;
}

.tensao-corrente {
    background-color: rgb(202, 47, 47);
}


.graficos {
    background-color: rgb(170, 44, 44);
}

.area-mapa {
    background-color: yellow;
}
</style>
