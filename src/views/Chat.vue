<template>


  <v-simple-table>
    <template 
    v-slot:default>

    
      <thead>
        <tr>

          <th class="text-center">
            no
          </th>
          <th class="text-center">
            출발지
          </th>

          <th class="text-center">
            목적지
          </th>

          <th class="text-center">
            시작일
          </th>

          <th class="text-center">
            종료일
          </th>

          <th class="text-center">
            카풀 요일
          </th>

          <th class="text-center">
            actions
          </th>

        </tr>
      </thead>


      <tbody>

          <tr
          v-for="driver in get_passenger_list" 
          :key="driver.name"
        >
          <td v-if="driver.name==='김인하'" class="text-center">{{ driver.carpool_id }}</td> 
          <td v-if="driver.name==='김인하'" class="text-center">{{ driver.starting_point }}</td>
          <td v-if="driver.name==='김인하'" class="text-center">{{ driver.destination_point }}</td>
          <td v-if="driver.name==='김인하'" class="text-center">{{ driver.start_date.substring(0,10) }}</td>
          <td v-if="driver.name==='김인하'" class="text-center">{{ driver.end_date.substring(0,10) }}</td>
          <td v-if="driver.name==='김인하'" class="text-center">{{ driver.dotw.join(',') }}</td> 
          <td v-if="driver.name==='김인하'" class="text-center"> 

          <v-btn
            color="primary"
            text
            @click="delete_driver(driver.carpool_id)"
          >
            삭제하기
          </v-btn>

      
    </td> 
  </tr>
          
          
      </tbody>
      
      
    </template>
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>김인하님이 요청받은 카풀 리스트</v-toolbar-title>

        
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
      </v-toolbar>
    </template>


            

  
  </v-simple-table>



</template>





<script>
import axios from "axios"


  export default {
    
      
    data: () => ({

      users: null,
      test2_data: null,

      get_passenger_list: [],

      dialog: false,


     
    }),



    

    created () {
      this.test();
      this.get_passenger();
      
    },

    methods: {
        test(){
        axios
        .get("https://dummyjson.com/products")
        .then(res => {
          console.log(res.data);
          this.test2_data=res.data.data
        })
        .catch(err => {
          console.log(err);
        });
        },

        test2(carpool_id){
        console.log(carpool_id)
        },
        

        get_passenger(){
        axios.get("http://ec2-3-37-128-210.ap-northeast-2.compute.amazonaws.com:3000/passenger",{params:{user_id:1}})
        .then(res => {
          console.log(res.data);
          console.log("get_passenger() 함수입니다. 김인하의 카풀 신청 목록을 불러옵니다.");
          this.get_passenger_list=res.data.data; 
          
        })
        .catch(err => {
          console.log(err);
          console.log("get_passenger() 함수 불러오기 실패 !");
        });

        },
      

     

      delete_driver(carpool_id) {
        axios
        .delete("http://ec2-3-37-128-210.ap-northeast-2.compute.amazonaws.com:3000/list/"+carpool_id, 
          {
            carpool_id: this.carpool_id,
            name: this.name,
            gender: this.gender,
            max_passenger: this.max_passenger,
            carpool_id: this.carpool_id,
            start_date: this.start_date,
            end_date: this.end_date,
            dotw: this.dotw,
            starting_point: this.starting_point,
            destination_point: this.destination_point,
            desired_arrival_time: this.desired_arrival_time,


          
        })
        .then(res => {
          console.log(res);
          console.log("id : " + carpool_id + " delete 성공");
          this.get_driver();
        })
        .catch(err => {
          console.log(err);
          console.log("id : " + carpool_id + " delete 실패");
        }); 

        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

     
    },
  }
   // https://vuetifyjs.com/en/components/data-tables/#crud-actions
</script>

