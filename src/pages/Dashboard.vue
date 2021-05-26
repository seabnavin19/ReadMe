<template>
  <div>
  
  
    <!--Stats cards-->
    
    <div  >
      <!-- <div class="col-md-6 col-xl-3" v-for="stats in statsCards" :key="stats.title">
        <stats-card>
          <div class="icon-big text-center" :class="`icon-${stats.type}`" slot="header">
            <i :class="stats.icon"></i>
          </div>
          <div class="numbers" slot="content">
            <p>{{stats.title}}</p>
            {{stats.value}}
          </div>
          <div class="stats" slot="footer">
            <i :class="stats.footerIcon"></i> {{stats.footerText}}
          </div>
        </stats-card>
      </div> -->
      
       <h4>Search For Customer</h4>
      <div class="d-flex col-6 mb-3 ">
       
        <input class="form-control  border border-dark" v-model="search" type="search" placeholder="Search Customer" aria-label="Search">
        <div class="col-1"></div>
        <button class="btn btn-outline-success" type="submit" > Search</button>
      </div>
    </div>
  
    
    <table class="table table-success table-striped h-25 ">
  <thead >
    <tr >
      <th scope="col" >Account Number</th>
      <th scope="col">Name</th>
      <!-- <th scope="col">Last</th>
      <th scope="col">Handle</th> -->
    </tr>
  </thead>
  
  <tbody>
   
       
    <tr v-for="(post,index) in filteredList" v-if="index<=5">
  
      <th scope="row">{{post.id}}</th>
      <td>{{post.name}}</td>

      <td><button class="btn btn-dark"> <router-link :to="{ name: 'stats', params: { id:post.id,name:post.name } }">View</router-link></button></td>

      <!-- <td>Otto</td>
      <td>@mdo</td> -->
    </tr>
    <!-- <tr v-if=""></tr> -->
       
  </tbody>
</table>
 <div class="row " v-if="load">
   <div class="col-5"></div>
    <div class="spinner-grow text-succeess align-centre" role="status">
  
</div>
<div class="spinner-grow text-secondary" role="status">

</div>
<div class="spinner-grow text-secondary" role="status">

</div>
  </div>
   
    <!--Charts hello-->
    <div class="row">
    <p class="h1">Customer Segmentation</p>
  
    </div>
    

    <!--Charts-->
    <div class="row fixed">
      

      <!-- <div class="col-12">
        <chart-card title="Users behavior"
                    sub-title="24 Hours performance"
                    :chart-data="usersChart.data"
                    :chart-options="usersChart.options">
          <span slot="footer">
            <i class="ti-reload"></i> Updated 3 minutes ago
          </span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Open
            <i class="fa fa-circle text-danger"></i> Click
            <i class="fa fa-circle text-warning"></i> Click Second Time
          </div>
        </chart-card>
      </div> -->

      <!-- <div class="col-md-6 col-12">
        <chart-card title="Email Statistics"
                    sub-title="Last campaign performance"
                    :chart-data="preferencesChart.data"
                    chart-type="Pie">
          <span slot="footer">
            <i class="ti-timer"></i> Campaign set 2 days ago</span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Open
            <i class="fa fa-circle text-danger"></i> Bounce
            <i class="fa fa-circle text-warning"></i> Unsubscribe
          </div>
        </chart-card>
      </div> -->
     

      <!-- <div class="col-md-6 col-12">
        
        <chart-card title="2015 Sales"
                    sub-title="All products including Taxes"
                    :chart-data="activityChart.data"
                    :chart-options="activityChart.options">
          
          <span slot="footer">
            <i class="ti-check"></i> Data information certified
          </span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Tesla Model S
            <i class="fa fa-circle text-warning"></i> BMW 5 Series
          </div>
        </chart-card>
      </div> -->

      <div class="col-md-6 col-xl-3" v-for="stats in statsCards" :key="stats.title">
        <stats-card>
          <div class="icon-big text-center" :class="`icon-${stats.type}`" slot="header">
            <i :class="stats.icon"></i>
          </div>
          <div class="numbers" slot="content">
            <p>{{stats.title}}</p>
            {{stats.value}}
          </div>
          <div class="stats" slot="footer">
            <i :class="stats.footerIcon"></i> {{stats.footerText}}
          </div>
        </stats-card>
      </div>

    </div>

  </div>
</template>
<script>
import { StatsCard, ChartCard } from "@/components/index";
import Chartist from 'chartist';
import db from '../components/firebaseInit';
import UserCard from "./UserProfile/UserCard.vue";




class Post {
  constructor(id, name) {
    this.id = id;
    this.name = name
    // this. = author;
    // this.img = img;
  }
}
export default {
  components: {
    StatsCard,
    ChartCard,
     UserCard,
    
  },

  computed: {
    filteredList() {
      return this.postList.filter(post => {
        
        return post.id.toLowerCase().includes(this.search.toLowerCase())
      })

     
     
      
    }
  },
  mounted() {
    db.collection('Bank').get().then((querySnapshot) => {
      
          querySnapshot.forEach((doc) => {
            // console.log(doc)
         
            var i;
            var l=[]
            for(i in doc.data()){
              // console.log(doc.data()[i])
              if(i.includes("user")){
                 this.sdata=new Post(doc.data()[i].AccountId,doc.data()[i].name)
               this.postList.push(this.sdata)
              console.log(i)
              }
             
              this.load=false
              
            }
            // this.sdata=doc.data()
            // console.log(this.sdata)

            
      
          })
        })
  },
  /**
   * Chart data used to render stats, charts. Should be replaced with server data
   */
  data() {
    return {
      load:true,
      sdata:'',
      
      statsCards: [
        {
          type: "warning",
          icon: "ti-user",
          title: "Group 1",
          value: "1178 customers",
          footerText: "Updated now",
          footerIcon: "ti-reload"
        },
        {
          type: "success",
          icon: "ti-user",
          title: "Group 2",
          value: "782 customers",
          footerText: "Last day",
          footerIcon: "ti-calendar"
        },{
          type: "primary",
          icon: "ti-user",
          title: "Group 1",
          value: "987 customers",
          footerText: "Updated now",
          footerIcon: "ti-reload"
        }
      ],
      usersChart: {
        data: {
          labels: [
            "9:00AM",
            "12:00AM",
            "3:00PM",
            "6:00PM",
            "9:00PM",
            "12:00PM",
            "3:00AM",
            "6:00AM"
          ],
          series: [
            [287, 385, 490, 562, 594, 626, 698, 895, 952],
            [67, 152, 193, 240, 387, 435, 535, 642, 744],
            [23, 113, 67, 108, 190, 239, 307, 410, 410]
          ]
        },
        options: {
          low: 0,
          high: 1000,
          showArea: true,
          height: "245px",
          axisX: {
            showGrid: false
          },
          lineSmooth: Chartist.Interpolation.simple({
            divisor: 3
          }),
          showLine: true,
          showPoint: false
        }
      },
      activityChart: {
        data: {
          labels: [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "Mai",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Nov",
            "Dec"
          ],
          series: [
            [542, 543, 520, 680, 653, 753, 326, 434, 568, 610, 756, 895],
            [230, 293, 380, 480, 503, 553, 600, 664, 698, 710, 736, 795]
          ]
        },
        options: {
          seriesBarDistance: 10,
          axisX: {
            showGrid: false
          },
          height: "245px"
        }
      },
      preferencesChart: {
        data: {
          labels: ["62%", "32%", "6%"],
          series: [62, 32, 6]
        },
        options: {}
      },
     search: '',
    postList : [
      
]

    };
  },
 
};
</script>
<style>
</style>
