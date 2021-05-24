<template>
    <!-- <card class="card" title="Customer's Profile">
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
    </card> -->
  <card class="card-user" title="Confession Fee">
      
    <div class="form-row">
      <div class="form-group col-md-6">
        <label for="number">Money of Transaction</label>
        <input type="number" class="form-control" placeholder="Money of Transaction" v-model="user.moneyOfTransaction">
      </div>
      <div class="form-group col-md-6">
        <label for="inputState">Service</label>
        <select id="selectedService" class="form-control">
          <option selected>Choose Service</option>
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
        <label>Calculated Confession Fee</label>
        <input type="number" class="form-control" placeholder="Confession Fee" v-model="user.calculatedFee">
      </div>
    </div>
    <!-- <div>
      <ul class="list-unstyled team-members">
        <li>
          <div class="row" v-for="member in members" :key="member.name">
            <div class="col-3">
              <div class="avatar">
                <img :src="member.image" alt="Circle Image" class="rounded img-fluid">
              </div>
            </div>
            <div class="col-6">
              {{member.name}}
              <br>
              <span :class="getStatusClass(member.status)">
                <small>{{member.status}}</small>
              </span>
            </div>

            <div class="col-3">
              <p-button type="success" outline icon>
                <i class="fa fa-envelope"></i>
              </p-button>
            </div>
          </div>
        </li>
      </ul>
    </div> -->
  </card>
</template>
<script>
export default {
  data() {
    return {
      user:{
        moneyOfTransaction : null,
        serviceChosen: null,
        calculatedFee: null,
        fixedOTT: null,
        fixedITT: null,
        

      }
    };
  },
  methods: {
    getFee(mOT){
      this.user.calculatedFee = this.user.fixedOTT
    },
    getStatusClass(selectedService) {
      switch (selectedService) {
        case "OTT":
          return this.getFee(this.user.moneyOfTransaction);
        case "ITT":
          return this.getFee(this.user,moneyOfTransaction);
        case "Water Bill":
          return this.getFee(this.user.moneyOfTransaction);
        case "EDC Bill":
          return this.getFee(this.user.moneyOfTransaction);
        default:
          return "text-success";
      }
    }
  }
};
</script>
<style>
</style>
