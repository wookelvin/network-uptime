<template>
  <div id="app">
    <div class="statusbox text-white" :class="(checked && online)?'bg-success':'bg-danger'" >
      <div v-if="checked">
        <div>Internet is</div>
        <div class="status-text" v-if="online">
          Online
        </div>  
        <div v-else class="status-text" >
          Offline
        </div>
      </div>
      
      <canvas id="chart" width="300" height="100" ref="canvas" class="mt-5"></canvas>
      
    </div>

  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Chart from 'chart.js';
import isOnline  from 'is-online';

@Component
export default class App extends Vue {
  online = false;
  checked = false;
  

  async checkOnline() {
    this.online = await isOnline();
    this.checked = true;
  }

  generateChart(){ 
    const ctx = this.$refs.canvas;
    const myChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
            datasets: [{
                label: '# of Votes',
                data: [12, 19, 3, 5, 2, 3],
                backgroundColor: [
                    'rgba(255, 99, 132, 1)',
                    'rgba(54, 162, 235, 1)',
                    'rgba(255, 206, 86, 1)',
                    'rgba(75, 192, 192, 1)',
                    'rgba(153, 102, 255, 1)',
                    'rgba(255, 159, 64, 1)'
                ],
                borderColor: [
                    'rgba(255, 99, 132, 1)',
                    'rgba(54, 162, 235, 1)',
                    'rgba(255, 206, 86, 1)',
                    'rgba(75, 192, 192, 1)',
                    'rgba(153, 102, 255, 1)',
                    'rgba(255, 159, 64, 1)'
                ],
                borderWidth: 1
            }]
        },
        options: {
            legend:{
              display: false
            },
            scales: {
                xAxes:[{
                    gridLines: {
                      display:true,
                      color: 'rgba(255,255,255,0.5)',
                    },
                    ticks:{
                      fontColor:'rgba(255,255,255,1)',
                    }
                }],
                yAxes: [{
                  
                    gridLines: {
                      display:true,
                      color: 'rgba(255,255,255,0.5)',
                      zeroLineColor: 'rgba(255,255,255,0.75)',
                    },
                    ticks: {
                        beginAtZero: true,
                        fontColor:'rgba(255,255,255,1)',
                    }
                }]
            }
        }
    });
  }
  mounted(){ 
    this.checkOnline();
    this.generateChart();
    setInterval(()=>{ 
      this.checkOnline();
    },5000);
  }


}
</script>


<style lang="scss">
@import 'src/scss/style.scss';
#app, body, html{
  height:100%;
}

.statusbox{ 
  height:100%;
  text-align: center;
  .status-text{
    font-size:3em;
    font-weight: bold;
  }
  display:flex;
  align-items:center;
  justify-content: center;
  flex-direction: column;
  padding: 2em;
}


</style>
