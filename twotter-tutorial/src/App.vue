<template>
  <div id="app">
  <nav>
    <router-link  to="/">
      <div class="navigation__logo">
        twitter
      </div>
    </router-link>

    <div class="navigation__user" v-if="user" >
      {{user.username}}
    </div>
    </nav>
    <router-view/>

  </div>

</template>

<script>
//import {reactive} from 'vue';
import {useStore} from 'vuex';
import {computed } from 'vue';
  export default {
  name: 'App',

    setup (){

      const store = useStore();
      const user = computed(()=>store.state.User.user);
      return {
        user
      }
    }


    // const state = reactive({
    //   user:{
    //     username : 'chinexman'
    //   }
    // })
    //   return {
    //   state
    //   }
    // }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

nav{
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 5%;
  background-color: deeppink;
  color: white;
  text-decoration: none;

}

.navigation__logo{
  font-weight: bold;
  font-size: 24px;
}
.navigation__user{
  font-weight: bold;
}
</style>
