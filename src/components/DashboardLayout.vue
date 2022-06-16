<template>
  <div class="full-width full-height">
    <div class="row justify-between q-pa-lg">
      <div class="col-3">
        <q-card>
          <div class="text-center q-pa-sm">
            <span><b>Avaliação média por corrida </b></span>
          </div>
          <div class="box-graph text-center">
            <span class="material-icons star-rate"> star_rate </span>
            <br />
            <span class="ratting-text"><b>4.5</b></span>
          </div>
        </q-card>
      </div>
      <div class="col-3">
        <q-card>
          <div class="text-center q-pa-sm">
            <span><b>Pessoas com mais carros</b></span>
          </div>
          <div class="box-graph">
            <table class="charts-css column datasets-spacing-4 chart">
              <tbody>
                <tr>
                  <td>Camille</td>
                </tr>
                <tr>
                  <td>Thiago</td>
                </tr>
                <tr>
                  <td>Hayana</td>
                </tr>
                <tr>
                  <td>Eduardo</td>
                </tr>
              </tbody>
            </table>
          </div>
        </q-card>
      </div>
      <div class="col-3">
        <q-card>
          <div class="text-center q-pa-sm">
            <span><b>Pessoas com mais carros</b></span>
          </div>
          <div class="box-graph">
            <table class="charts-css column datasets-spacing-4 chart">
              <tbody>
                <tr>
                  <td>Camille</td>
                </tr>
                <tr>
                  <td>Thiago</td>
                </tr>
                <tr>
                  <td>Hayana</td>
                </tr>
                <tr>
                  <td>Eduardo</td>
                </tr>
              </tbody>
            </table>
          </div>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script>
import "charts.css";
export default {};
</script>

<style>
.box-graph {
  height: 170px !important;
  padding: 10px;
}

.star-rate {
  font-size: 100px;
  color: rgba(255, 220, 90, 0.75);
}

.ratting-text {
  font-size: 35px;
}
</style>
