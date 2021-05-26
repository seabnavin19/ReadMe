<template>
  <card class="card-user" title="Customer's Profile">
    <div>
      <form @submit.prevent>
        <div class="row">
          <div class="col-md-6">
            
            <fg-input type="text"
                      label="Username"
                      placeholder="Username"
                      v-model="user.username">
            </fg-input>
          </div>
          <div class="col-md-6">
            <fg-input type="text"
                      label="Account Number"
                      placeholder="Account Number"
                      v-model="user.accountNumber">
            </fg-input>
          </div>
        </div>
        <div class="row">
          <div class="col-md-6">
            <fg-input type="text"
                      label="Cards obtained"
                      placeholder="Number of cards"
                      v-model='user.has_credit_card'>
            </fg-input>
          </div>
          <div class="col-md-6">
            <fg-input type="text"
                      label="Year with Bank"
                      placeholder="Tenure"
                      v-model="user.tenure">
            </fg-input>
          </div>
        </div>
        <div class="row">
          <div class="col-md-4">
            <fg-input type="text"
                      label="Balance"
                      placeholder="Balance"
                      v-model="user.balance">
            </fg-input>
          </div>
                    <div class="col-md-4">
            <fg-input type="text"
                      label="Group"
                      placeholder="Group"
                      v-model="user.group">
            </fg-input>
          </div>
                    <div class="col-md-4">
            <fg-input type="text"
                      label="Number of Product"
                      placeholder="Number of product"
                      v-model="user.numberOfProduct">
            </fg-input>
          </div>
        </div>
        <div class="row">
          <div class="col-md-12">
            <div class="form-group">
              <label> Customer's Special Offer</label>
              <textarea rows="5" class="form-control border-input"
                        placeholder="Special Offer"
                        v-model="user.specialOffer">
              </textarea>
            </div>
          </div>
        </div>
        <div class="text-center">
          <p-button type="info"
                    round
                    @click.native.prevent="updateProfile">
            Update Profile
          </p-button>
        </div>
        <div class="clearfix"></div>
      </form>
    </div>
  </card>
</template>

<script>

import db from "../../components/firebaseInit"

export default {
  data() {
    return {
      user: {
        age:null,
        gender:null,
        group: null,
        balance: null,
        numberOfProduct: null,
        has_credit_card: null,
        salary: null,
        // billEDC: null,
        // billCleanWater: null,
        // phoneNumber: "087555087",
        username: null,
        accountNumber: null,
        firstName: null,
        lastName: null,
        specialOffer: null,
        tenure: null,
      }
    };
  },
  methods: {
    updateProfile() {
      alert("Your data: " + JSON.stringify(this.user));
     
    }
  },
  mounted() {
    if(this.$route.params.id){
      this.user.accountNumber = this.$route.params.id;
    }
    db.collection('Bank').get().then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            
          
            console.log(doc)
            var i;
            var l=[]
            for(i in doc.data()){
              // console.log(doc.data()[i])
              // this.sdata=new Post(doc.data()[i].AccountId,doc.data()[i].name)
              // this.postList.push(this.sdata)
              
              if(doc.data()[i].AccountId == this.user.accountNumber){
                var customer = doc.data()[i]
                this.user.username = customer.name
                this.user.specialOffer = customer.special_offer
                this.user.group = parseInt(customer.Group) +1
                this.user.numberOfProduct = customer.NumOfProducts
                this.user.balance = customer.Balance + " $"
                this.user.has_credit_card = customer.HasCrCard 
                this.user.salary = customer.EstimatedSalary
                this.user.tenure = customer.Tenure + " year"
                break

                
                // console.log
              }


            }
            

            
      
          })
        })
     
      
    
  },
};
</script>
<style>
</style>
