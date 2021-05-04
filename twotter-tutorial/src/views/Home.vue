<template>
  <div class="home">
   <h1>Home</h1>
    <div class="user-link">
      <router-link v-for="user in users" :to="{name:'userProfile',params:{userId:user.id}}" :key="user.id">
        {{user.username}}
        <p></p>
      </router-link>
    </div>
  </div>
</template>

<script>
    import {users}  from '../assets/users';

export default {
  name: 'Home',
  setup() {
    return {
users
}
}
}
</script>


<style>
.home {

  padding: 50px 5%;
}
.user-link{
  display: flex;
  flex-direction: column;
}
</style>