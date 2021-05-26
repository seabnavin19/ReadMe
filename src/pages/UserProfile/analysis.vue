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
  <h4>{{churn}}%</h4>
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
import db from "../../components/firebaseInit"

  export default {
  components: { 
    Card ,
    RadialProgressBar

  },
    data() {
      return {
        accountNumber : null,
        home_loan :null,
        group:null,
        personal_loan :null,
        personal_cheque : null,
        fast_saver :null,
        one_card : null,
        churn:null,
        completedSteps: 1,
        totalSteps: 1,
        bars: [
          { variant: 'Home Loan', value:0 },
          { variant: 'Personal Loan', value:0 },
          { variant: 'Fast Saver', value: 20 },
          { variant: 'The One', value: this.personal_cheque },
          { variant: 'Personal Cheque', value: this.fast_saver },
        ],
        timer: null
      }
    },
    mounted() {
    if(this.$route.params.id){
      this.accountNumber = this.$route.params.id;
    }
    db.collection('Bank').get().then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            // console.log(doc)
            var i;
            
            var l=[]
            
            for(i in doc.data()){
              if(doc.data()[i].AccountId == this.accountNumber){
                var customer = doc.data()[i]
                this.group = parseInt(customer.Group) +1 
                console.log(this.group)
                break
              }

              if (i == "Group"+this.group ){
                console.log(i)
                console.log('Group'+this.group)
                var user = doc.data()[i].Service
                // console.log(user)
                  this.bars[0].value = user.home_load
                  this.bars[1].value = user.personal_loan
                  this.bars[2].value= user.Fast_Saver
                  this.bars[3].value = user.The_ONE
                  this.bars[4].value = user.Personal_Cheque
              }
              // console.log(doc.data()[i])
              // this.sdata=new Post(doc.data()[i].AccountId,doc.data()[i].name)
              // this.postList.push(this.sdata)
              
              if(doc.data()[i].AccountId == this.$route.id){
                var customer = doc.data()[i]
                this.completedSteps=customer.Churn*100
                this.churn=parseFloat(this.completedSteps).toFixed(2) 
                break
              }
              
            }
          })
        })
  },
    beforeDestroy() {
      clearInterval(this.timer)
      this.timer = null
    }
  }
</script>