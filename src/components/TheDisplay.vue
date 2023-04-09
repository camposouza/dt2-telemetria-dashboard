<template>
    <div class="container">
        <div class="visor">
            <div class="valor">
                <span class="tensao">0.00</span>
                <span class="unit-display"> V</span>
                <div class="legenda">Tensão</div>
            </div>
        </div>
        <div class="visor">
            <div class="valor">
                <span class="corrente">0.00</span>
                <span class="unit-display"> A</span>
            </div>
            <div class="legenda">Corrente</div>
        </div>
    </div>
</template>

<script>
import $ from 'jquery';

export default {
  name: 'TheDisplay',
  data() {
    return {
      tensao: 0.00,
      corrente: 0.00
    };
  },
  created() {
    this.getValues();
  },
  methods: {
    alteraTensao(tensao) {
      $('.tensao').text(tensao)
    },
    alteraCorrente(corrente) {
      $('.corrente').text(corrente)
    },
    getValues() {
        const self = this;
        setInterval(() => { // Ajax request at each time interval
          $.ajax({
            url: '../php/db_query_ina226.php',
            type: 'POST',
            dataType: 'json',
            success: function (result) {
              self.alteraTensao(result.voltage_battery);
              self.alteraCorrente(result.current_motor);
            },
          });
        }, 500);
  }
}
}
</script>

<style scoped>
.container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    text-align: center;
    position: relative
}

.valor {
    font-size: 50px;
}

.unit-display {
    font-size: 40px;
}

.legenda {
    font-size: 25px;
}
</style>