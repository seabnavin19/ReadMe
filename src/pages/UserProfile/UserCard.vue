<template>
  <card class="card-user">
    <!-- <div slot="image">
      <img src="@/assets/img/background.jpg" alt="...">
    </div> -->
    <div>
      <div class="author">
        <img class="avatar border-white" src="@/assets/img/faces/huameng.jpg" alt="...">
        <h4 class="title">HuaMengLim
          <br>
          <a href="#">
            <small>@huamenglim</small>
          </a>
        </h4>
      </div>
      <!-- <p class="description text-center">
        "I like the way you work it
        <br> No diggity
        <br> I wanna bag it up"
      </p> -->
    </div>
    <hr>
    <div class="text-center">
      <div class="row">
        <div v-for="(info, index) in details" :key="index" :class="getClasses(index)">
          <h5>{{info.title}}
            <br>
            <small>{{info.subTitle}}</small>
          </h5>
        </div>
      </div>
    </div>
  </card>
</template>
<script>
import db from "../../components/firebaseInit"
class User{
  constructor(name,age,gender) {
    this.age = age;
    this.name = name;
    this.gender = gender;
    // this. = author;
    // this.img = img;
  }
}
export default {
  data() {
    return {
      user:null,
    
      // accountStatus: "Active",
      details: [
        {
          title: this.user.age,
          subTitle: "Age"
        },
        {
          title: this.user.gender,
          subTitle: "Gender"
        },
        {
          title:"Active",
          subTitle: "Status"
        }
      ]
    };
  },
  methods: {
    getClasses(index) {
      var remainder = index % 3;
      if (remainder === 0) {
        return "col-lg-3 offset-lg-1";
      } else if (remainder === 2) {
        return "col-lg-4";
      } else {
        return "col-lg-3";
      }
    }
  },
  mounted() {
    this.user=new User(19,"Male","userName")
    // console.log(this.user.userName)
    // if(this.$route.params.id){
    //   this.user.accountNumber = this.$route.params.id;
    // }
    db.collection('Bank').get().then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
          
            // console.log(doc.data())
            var i;
            var l=[]
            for(i in doc.data()){
              // console.log(doc.data()[i])
              // this.sdata=new Post(doc.data()[i].AccountId,doc.data()[i].name)
              // this.postList.push(this.sdata)
              
              if(doc.data()[i].AccountId == this.user.accountNumber){
                var customer = doc.data()[i]
                this.user.userName = customer.name
                this.user.gender = customer.Gender
                this.user.age = customer.Age
                // this.numberOfProduct = customer.NumOfProducts
                // this.balance = customer.Balance
                // this.has_credit_card = customer.HasCrCard
                // this.salary = customer.EstimatedSalary
                // this.tenure = customer.Tenure

                
                // console.log
              }
            }      
          })
        })
  }
};
</script>
<style>
</style>