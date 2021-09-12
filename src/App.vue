<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app class="montserrat-alternates">
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="montserrat-alternates drawer-title color-black"> Coffee Record </v-list-item-title>
          <v-list-item-subtitle class="color-purple"> What is your fav? </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="color-purple">{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      app
      prominent
      src='./assets/coffee_01.jpg'
    >
      <template v-slot:img='{ props }'>
        <v-img
          v-bind='props'
          gradient='to top right, rgba(174, 156, 148, .7), rgba(253, 244, 231, 1)'
        ></v-img>
      </template>

      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-app-bar-title class="font-weight-bold montserrat-alternates color-black">Coffee Record</v-app-bar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container fluid class="pa-0">
        <router-view></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
      { title: 'About', icon: 'mdi-help-box', to: '/about' }
    ]
  })
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat+Alternates:wght@100;200;300;400;500;600;700;800&display=swap');
  .montserrat-alternates{
    font-family: 'Montserrat Alternates', sans-serif;  }
  .drawer-title{
    font-size: 20px;
    font-weight: 600;
  }
  .color-black{
    color: #36312E;
  }
  .color-purple{
    color: #716679;
  }
  .color-baige{
    color: #FDF4E7;
  }
  .color-brown{
    color: #AE9C94;
  }
  .color-green{
    color: #93A8B2;
  }
</style>