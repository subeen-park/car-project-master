<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="white"
      flat
      src="car-image.jpg"
      height="100px" 
    >
      <v-container class="py-0 fill-height">
        

        <v-btn
          v-for="item in top1"
          :key="item.title"
          :to="item.to"
          text
        >
          {{ item.title }}
        </v-btn>

        <v-spacer></v-spacer>

        
      </v-container>
    </v-app-bar>

    

    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <v-col cols="2">
            <v-sheet rounded="lg">
              
              <v-list 
              rounded
              >

              

        <v-list-item link>
          <v-list-item-content>
            <v-list-item-title class="text-h6">
              <v-btn v-if="login_num==1" @click="login()"> Login </v-btn>
              <v-spacer> </v-spacer>
              <v-spacer> </v-spacer>
              {{login_name}}
            </v-list-item-title>
            <v-list-item-subtitle>{{login_com}}</v-list-item-subtitle>
          </v-list-item-content>

          
        </v-list-item>
        <v-divider class="my-2"></v-divider>

                <v-list-item
                  v-for="item in items1"
                  :key="item.title"
                  :to="item.to"
                  link
                >

                  <v-list-item-content>
                    <v-list-item-title>
                      {{item.title}}
                    </v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
               



                  
            <v-list-group
            v-for="item in items2"
            :key="item.title"
            v-model="item.active"
            
            >


        <template v-slot:activator>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"></v-list-item-title>
          </v-list-item-content>
        </template>

        <v-list-item
         
          v-for="child in item.items"
          :key="child.title"
          :to="child.to"
          link
        >


          <v-list-item-content>
            <v-list-item-title v-text="child.title"></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-group>


      <v-list-group
            v-for="item in items3"
            :key="item.title"
            v-model="item.active"
            
            >


        <template v-slot:activator>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"></v-list-item-title>
          </v-list-item-content>
        </template>

        <v-list-item
         
          v-for="child in item.items_3"
          :key="child.title"
          :to="child.to"
          link
        >


          <v-list-item-content>
            <v-list-item-title v-text="child.title"></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-group>

      </v-list>

                  
               
            </v-sheet>
          </v-col>

          <v-col>
            <v-sheet
              min-height="70vh"
              rounded="lg"
            >
              <router-view></router-view>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>




<script>
import Home from './views/Home.vue'
  export default {
    components:{
      Home
    },
    data() {
      return {
      login_login:"Login",
      login_name:"",
      login_com:"",
      login_num : 1,
      items1:[
        { title: 'Home', icon: 'mdi-view-dashboard', to: '/'}], // 메인 화면. 검색필터 있음 
      items2: [ 
        {
          action: 'mdi-account', // 마이페이지, 아이콘
          active: false,
          items: [
            
            { title: 'Passenger', to: '/passenger' },
            { title: 'Driver', to: '/driver' },
            //{ title: 'Request', to: '/request' },
            { title: 'Chat', to: '/chat' },
            { title: 'Past', to: '/past' },
            
          ],
          title: 'Mypage'
          
        }
    
        ],
      items3: [{
        items_3:[
          
        {title: '보낸 요청', to:'/request'},
        {title: '받은 요청', to:'/request2'},
        ],
        title: 'Carpool'
      }
      ],
        
        top1:[
        { title: ' INFORMATION ABOUT MYPAGE ', icon: 'mdi-view-dashboard', to: '/info'},
        ],
      
      drawer:false,
     }
    },
    methods: {
      login(){
        this.login_login="Logout"
        this.login_name="김인하"
        this.login_com="OO전자"
        this.login_num = 0;
      },
    }
  }
</script>