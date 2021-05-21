<template>
  <card class="card" title="Customer's Profile">
    <div>
      <form @submit.prevent>
        <div class="row">
          <div class="col-md-5">
            <!-- <fg-input type="text"
                      label="Company"
                      :disabled="true"
                      placeholder="Paper dashboard"
                      v-model="user.company">
            </fg-input> -->
            <fg-input type="text"
                      label="Username"
                      placeholder="Username"
                      v-model="user.username">
            </fg-input>
          </div>
          <div class="col-md-3">

            <fg-input type="number"
                      label="Phone Number"
                      placeholder="Phone Number"
                      v-model="user.phoneNumber">
            </fg-input>
          </div>
          <div class="col-md-4">
            <fg-input type="number"
                      label="Account Number"
                      placeholder="Account Number"
                      v-model="user.accountNumber">
            </fg-input>
          </div>
        </div>

        <div class="row">
          <div class="col-md-3">
            <fg-input type="text"
                      label="First Name"
                      placeholder="First Name"
                      v-model="user.firstName">
            </fg-input>
          </div>
          <div class="col-md-3">
            <fg-input type="text"
                      label="Last Name"
                      placeholder="Last Name"
                      v-model="user.lastName">
            </fg-input>
          </div>
          <div class="col-md-6">
            <fg-input type="text"
                      label="Address"
                      placeholder="Address"
                      v-model="user.address">
            </fg-input>
          </div>
        </div>

        <div class="row">
          <div class="col-md-4">
            <fg-input type="number"
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
            <fg-input type="number"
                      label="Number of Product"
                      placeholder="Number of product"
                      v-model="user.numberOfProduct">
            </fg-input>
          </div>
        </div>

        <div class="row">
          <div class="col-md-4">
            <fg-input type="number"
                      label="Salary/Income"
                      placeholder="Income"
                      v-model="user.salary">
            </fg-input>
          </div>
          <div class="col-md-4">
            <fg-input type="number"
                      label="Electricity Bill"
                      placeholder="Electricity Bill"
                      v-model="user.billETC">
            </fg-input>
          </div>
          <div class="col-md-4">
            <fg-input type="number"
                      label="Clean Water Bill"
                      placeholder="Clean Water Bill"
                      v-model="user.billCleanWater">
            </fg-input>
          </div>
        </div>

        <div class="row">
          <div class="col-md-12">
            <div class="form-group">
              <label> Customer Description</label>
              <textarea rows="5" class="form-control border-input"
                        placeholder="Here can be your description"
                        v-model="user.customerDescription">

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
export default {
  data() {
    return {
      user: {
        gender:null,
        group: null,
        balance: null,
        numberOfProduct: null,
        has_credit_card: null,
        // OTT_minFee: null,
        // OTT_maxFee: null,
        // OTT_cableFee: null,
        // ITT_minFee: null,
        // ITT_maxFee: null,
        // ITT_cableFee: null,
        salary: null,
        billETC: null,
        billCleanWater: null,
        phoneNumber: "087555087",
        username: "Huameng Lim",
        accountNumber: "1101901058",
        firstName: "Lim",
        lastName: "HuaMeng",
        address: "Kirirom Institute of Technology, Kompong Speu, Cambodia",
        city: "Kompongspeu",
        postalCode: "12100",
        customerDescription: 'A second year student majoring in software Engineering.'
      }
    };
  },
  methods: {
    updateProfile() {
      alert("Your data: " + JSON.stringify(this.user));
    }
  }
};
</script>
<style>
</style>
