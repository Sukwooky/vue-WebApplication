<template>

   <!-- v-bind="$attrs"를 통해 상위 props를 내려받음 -->
   <!-- <v-navigation-drawer v-model="drawer" :src="require('@/assets/sidebar.jpg')" dark app> -->
  <v-navigation-drawer v-bind="$attrs" :src="require('@/assets/sidebar.jpg')" dark app>

      <!--(1)v-navigation-drawer :src="require('@/assets/sidebar.jpg')"[배경입히기]-->
      <!--(2)v-navigation-drawer 배경이미지[그라디언트 취하기]-->
      <!--(3)v-navigation-drawer dark[글자 밝게하기]-->
      <!--(4)v-navigation-drawer active-class="primary"[선택시 색깔 표시]-->

      <!--하위컴포넌트에서 slot을 이용해 해당부분에 삽입-->
      <!--상위컴포넌트--> 
      <template v-slot:img="props">
        <v-img :gradient="gradient" v-bind="props"></v-img>
      </template>

      <!--drawer 제목, 부제목-->
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title>
            건강관리 서비스
          </v-list-item-title>
          <v-list-item-subtitle>
            영양갱
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <!--drawer Navigation-->
      <v-list expand dense nav>
        
        <template v-for="(item,index) in items">
          
          <!--item.items가 존재하면O-->
          <v-list-group v-if="item.items" :key="index" :prepend-icon="item.icon">
            
            <!--주 Navigtaion-->
            <template #activator>
              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item-content>
            </template>

            <!--보조 Navigtaion-->
            <template v-for="(itemchild, index) in item.items">
              <!--item-->
              <v-list-item :key="index" :to="itemchild.to" link>
                <v-list-item-icon>
                  <v-icon>{{ itemchild.icon }}</v-icon>
                </v-list-item-icon>

                <v-list-item-content>
                  <v-list-item-title>{{ itemchild.title }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </template>

          </v-list-group>

          <!--item.items가 존재하면X-->
          <!--item-->
          <v-list-item v-else :key="index" :to="item.to" active-class="primary" link>
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>

        </template>


      </v-list>

    </v-navigation-drawer>
</template>

<script>
export default {
  name : "AppNavigationDrawer",
  data() {
    return {
      gradient: "rgba(0,0,0,0.7), rgba(0,0,0,0.7)",

      items: [
        { title: 'Dashboard', icon: 'mdi-view-dashboard', to: "/" },
        { title: '로그인', icon: 'mdi-account-badge', to: "/authentication/sign-in" },
        { title: '회원가입', icon: 'mdi-apple-finder', to: "/authentication/info-first" },
        { title: '마이페이지', icon: 'mdi-elephant', items : [
            { title: "다이어리", icon: 'mdi-heart-box-outline', to: "/mypage/diary" },
            { title: "리포트", icon: 'mdi-history', to: "/mypage/report" },
        ]},     

        { title: 'Pages', icon: 'mdi-menu', items : [
            { title: "연습", icon: 'mdi-clipboard-list-outline', to: "/page/restaurantList" },
        ]},      
        
        { title: '추천받기', icon: 'mdi-thumb-up-outline', items : [
            { title: "메뉴 추천", icon: 'mdi-silverware', to: "/recommend/menu" },
            { title: "음식점 추천", icon: 'mdi-home-variant', to: "/recommend/restaurant" },
        ]},   
      ],
    }
  }
}
</script>

<style>

</style>