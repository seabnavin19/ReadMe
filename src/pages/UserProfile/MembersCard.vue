<template>

  <card class="card-user" title="Confession Fee">

    <div class="form-row">


      <div class="form-group col-md-6">
 
        <label for="number">Money of Transaction</label>
        <input type="number" class="form-control" placeholder="Money of Transaction" v-model="moneyOfTransaction" >
 
      </div>


      <div class="form-group col-md-6">

        <label for="inputState">Service</label>

        <select id="selectedService" class="form-control" v-model="selectedService">

          <option selected  >Choose Service</option>
          <option>OTT</option>
          <option>ITT</option>
          <option>Water Bill</option>
          <option>EDC Bill</option>
          <option>Other Services</option>

        </select>

      </div>


    </div>

    <div class="form-row">

      <div class="form-group col-md 6">

        <label>Minimum Fee</label>
        <input type="number" class="form-control" placeholder="Minimum Fee" v-model="minFee">

      </div>
      <div class="form-group col-md 6">

        <label>Maximum Fee</label>
        <input type="number" class="form-control" placeholder="Maximum Fee" v-model="maxFee">

      </div>
    
    </div>

    <div class="form-row">

      <div class="form-group col-md 6">

        <label>Calculated Confession Fee</label>
        <input type="number" class="form-control" placeholder="Confession Fee" v-model="calculatedFee">

      </div>

      <div class="form-group col-md 6">

        <label>Commission Fee</label>
        <input type="number" class="form-control" placeholder="Commission Fee" v-model="comFee">

      </div>
    
    </div>

    <div class="row">
        <div class="col-5"></div>
        <button type="submit" class="btn btn-primary " @click="getStatusClass(selectedService)">submit</button>
    </div>

  </card>
  
</template>
<script>
import db from "../../components/firebaseInit"

export default {

  data() {
    return {
        minFee:null,
        maxFee:null,
        comFee:null,
        moneyOfTransaction :null,

        selectedService: null,
        calculatedFee: null,

      OTT:{
        minFee:null,
        maxFee:null,
        comFee:null
      },
      ITT:{
        minFee:null,
        maxFee:null,
        comFee:null
      },
      Bill:{
        comFee:null
      }
    };
  },
  mounted() {
    
    db.collection('Bank').get().then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
          
            console.log(doc)
            var i;
            var l=[]
            for(i in doc.data()){
              // console.log(doc.data()[i])
              // this.sdata=new Post(doc.data()[i].AccountId,doc.data()[i].name)
              // this.postList.push(this.sdata)
              
              if(doc.data()[i].AccountId == this.$route.params.id){
                var customer = doc.data()[i].OTT
                this.OTT.minFee=customer.Min_Fee
                this.OTT.maxFee=customer.Max_Fee
                this.OTT.comFee=customer.comision

                var customer1 = doc.data()[i].ITT
                this.ITT.minFee=customer1.Min_Fee
                this.ITT.maxFee=customer1.Max_Fee
                this.ITT.comFee=customer1.comision
                break

              }
            }
            
          })
        })
     
  
   
  },
  methods: {
    getFee(money,com,min,max){
      console.log(com)
      this.calculatedFee = money*com
      if(this.calculatedFee<=min){
        this.calculatedFee=min
      }
      return this.calculatedFee
      
    },
    
    getStatusClass(selectedService) {
      
      switch (selectedService) {
        case "OTT":
          this.minFee = this.OTT.minFee
          this.maxFee = this.OTT.maxFee
          this.comFee = this.OTT.comFee
          return this.getFee(this.moneyOfTransaction,this.OTT.comFee/100,this.OTT.minFee,this.OTT.maxFee);
        case "ITT":
          this.minFee = this.ITT.minFee
          this.maxFee = this.ITT.maxFee
          this.comFee = this.ITT.comFee
          return this.getFee(this.moneyOfTransaction, this.ITT.comFee/100, this.ITT.minFee, this.ITT.maxFee);
        case "Water Bill":
          this.minFee = 0
          this.maxFee = 0
          this.comFee = 0
          return this.getFee(this.moneyOfTransaction, 0, 0, 0);
        case "EDC Bill":
          this.minFee = 0
          this.maxFee = 0
          this.comFee = 0
          return this.getFee(this.moneyOfTransaction, 0, 0, 0);
        default:
          return "text-success";
      }
    }
  }
};
</script>
<style>
</style>
