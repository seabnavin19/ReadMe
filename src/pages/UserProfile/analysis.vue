<template>
<card >
  <div>
    <h2>
      Predictive Analysis
    </h2>
  </div>
  <div class="p-5 row">
    <div class="col-3"></div>
  <radial-progress-bar  :diameter="200"
                       :completed-steps="completedSteps"
                       :total-steps="totalSteps"
                       :innerStrokeColor="ffffff">
                      
  <h2>Churn</h2>
  <h4>10%</h4>
  </radial-progress-bar>
  </div>
  <div>
    <h2>Services</h2>
    <div v-for="bar in bars" class="row m-5">
      <div class="col-sm-2">{{ bar.variant }}:</div>
      <div class="col-sm-10 pt-3">
        <b-progress :value="bar.value" :variant="bar.variant" :key="bar.variant" ></b-progress>
      </div>
    </div>
  </div>
</card>
</template>

<script>
import Card from '../../components/Cards/Card.vue'
import RadialProgressBar from 'vue-radial-progress'
  export default {
  components: { 
    Card ,
    RadialProgressBar
  },
    data() {
      return {
        completedSteps: 1,
      totalSteps: 10,
        bars: [
          { variant: 'Home Loan', value: 75 },
          { variant: 'Personal Loan', value: 75 },
          { variant: 'One Card', value: 75 },
          { variant: 'danger', value: 75 },
        ],
        timer: null
      }
    },
    mounted() {
      
    },
    beforeDestroy() {
      clearInterval(this.timer)
      this.timer = null
    }
  }
</script>