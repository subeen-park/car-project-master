<template>


  <v-simple-table>
    <template 
    v-slot:default>

    
      <thead>
        <tr>

          <th class="text-center">
            이름
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
            도착시간
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
          v-for="driver in get_driver_list" 
          :key="driver.carpool_id"
        >
          <td  class="text-center">{{ driver.driver_name }}</td> 
          <td  class="text-center">{{ driver.starting_point }}</td>
          <td class="text-center">{{ driver.destination_point }}</td>
          <td  class="text-center">{{ driver.start_date.substring(0,10) }}</td>
          <td  class="text-center">{{ driver.end_date.substring(0,10) }}</td>
          <td  class="text-center">{{ driver.desired_arrival_time.substring(0,5)}}</td>
          <td  class="text-center">{{ driver.dotw.join(',') }}</td> 
          <td  class="text-center"> 

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
        <v-toolbar-title>김인하님이 탑승자로 등록된 카풀 리스트</v-toolbar-title>

        
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

      get_driver_list: [],

      dialog: false,


     
    }),



    

    created () {
      this.get_driver();
      
    },

    methods: {
        

        get_driver(){
        axios
        .get("http://ec2-3-37-128-210.ap-northeast-2.compute.amazonaws.com:3000/passenger?user_id=1")
        .then(res => {
          console.log(res.data);
          console.log("get_driver() 함수입니다. 김인하의 카풀 목록을 불러옵니다.");
          this.get_driver_list=res.data.data  
          
        })
        .catch(err => {
          console.log(err);
        });

        },
      

     

      delete_driver(carpool_id) {
        axios
        .post("http://ec2-3-37-128-210.ap-northeast-2.compute.amazonaws.com:3000/delete/carpool",
          {
            carpool_id: carpool_id
        })
        .then(res => {
          console.log(res);
          console.log("id : " + carpool_id + " delete 성공");
          alert("삭제되었습니다.")
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

