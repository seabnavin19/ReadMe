<template>
<div>
<analysis></analysis>
 <div class="row">
   
   
    <div class="col-md-6 col-12">
      <div slot="legend " class="m-5">
            <i class="fa fa-circle text-info"></i> Open
            <i class="fa fa-circle text-danger"></i> Bounce
            <i class="fa fa-circle text-warning"></i> Unsubscribe
          </div>
        <chart-card title="Gender"
                    sub-title="Last campaign performance"
                    :chart-data="preferencesChart.data"
                    chart-type="Pie">
          <span slot="footer">
            <i class="ti-timer"></i> Campaign set 2 days ago</span>
          
        </chart-card>

      </div>
      
  

  
  
 </div>
</div>
</template>
<script>
import { StatsCard, ChartCard } from "@/components/index";
import Chartist from 'chartist';
import db from '../components/firebaseInit';
import analysis from "./UserProfile/analysis.vue"

export default {
  data() {
    return {

       preferencesChart: {
        data: {
          labels: ["62%", "32%", "6%"],
          series: [62, 32, 6]
        },
        options: {}
      },
    }
  },
  components: {
    StatsCard,
    analysis,
    ChartCard },

};
</script>
<style>
</style>
