<template>

    <div class="row">
      
      <div class="col-xl-4 col-lg-5 col-md-6">
    
        <user-card>

        </user-card>
        <members-card>

        </members-card>
      </div>
      <div class="col-xl-8 col-lg-7 col-md-6">
        <edit-profile-form>

        </edit-profile-form>
        <analysis>
          
        </analysis>
      </div>
    </div>
</template>
<script>
import EditProfileForm from "./UserProfile/EditProfileForm.vue";
import UserCard from "./UserProfile/UserCard.vue";
import analysis from "./UserProfile/analysis.vue"
import MembersCard from "./UserProfile/MembersCard.vue";
import db from "../components/firebaseInit"
export default {
  
  components: {
    EditProfileForm,
    UserCard,
    analysis,
    MembersCard
  },
  mounted() {
    
    
  },
};
</script>
<style>
</style>
