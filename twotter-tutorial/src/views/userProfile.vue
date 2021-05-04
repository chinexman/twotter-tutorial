<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@_{{state.users.username}}{{state.users.userwork}}</h1>
<!--      <h2>{{userId}}</h2>-->
      <div class="user-profile__admin-bagde" v-if="state.users.isadmin">
        admin
      </div>
      <div class="user-profile__admin-bagde" v-else>
        not admin
      </div>
      <div class="user-profile__followers-count">
        <strong>followers:</strong><br>
        {{state.followers}}
      </div>
      <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot" :class="{'--exceeded':newTwootCharacterCount>180}">
        <label for="newTwoot"><strong>New Twoot:</strong>{{newTwootCharacterCount}}/180</label>
        <textarea id="newTwoot" rows="4" v-model="state.newTwootContent"></textarea>
        <div class="user-profile__create-type">
          <label for="newTwootType"><strong>Type: </strong></label>
          <select id="newTwootType" v-model="state.selectedTwootType">
            <option :value="option.value" v-for="(option,index) in state.twootTypes" :key="index">
              {{option.name}}
            </option>
          </select>
        </div>
        <button>
          twoot!
        </button>
      </form>
    </div>

    <div class="user-profile__twoots-wrapper">

      <twootitem
          v-for="twoot in state.users.twoots"
          :key="twoot.id"
          :username="state.users.username"
          :twoot="twoot"
          v-on:favourite="togglefavourite"></twootitem>
   </div>
  </div>
</template>
<script>
  import Twootitem from "../components/twootitem";
  import { users}  from '../assets/users';

  import {useRoute } from 'vue-router';
  import { reactive, computed} from "vue";
export default {
  name: 'user-profile',
  components: {Twootitem},
  setup()  {
    const route = useRoute();
    const userId = computed(()=>route.params.userId)

    const state = reactive({
      newTwootContent:"",
      selectedTwootType:'instant',
      twootTypes: [
        { value:'draft', name:"Draft"},
        { value:'instant', name:"Instant Twoot"}
      ],
      followers: 0,
     users:users[userId.value] || users[1]

      //we are not using this anymore, making it user defined from api or database
      // users: {
      //   id: 1,
      //   username: 'chinexman',
      //   firstname: 'chinedu',
      //   lastname: 'emordi',
      //   email: 'chineduemordi@gmail.com',
      //   userwork:'developer',
      //   isadmin: true,
      //   twoots: [
      //     {
      //       id: 1,
      //       content: 'tweeter is amazing'
      //     },
      //     {
      //       id: 2,
      //       content: 'Dont forget to subscribe to my youtube channerl more light'
      //     }
      //   ]
      // }
    })
   const  newTwootCharacterCount = computed(()=> state.newTwootContent.length)

    function followUser () {
      this.oldfollowers = this.followers
      this.followers++
    }

    function togglefavourite(id) {

      console.log(`favourite twoot ${id}`)
    }

    function createNewTwoot() {
      if(state.newTwootContent && state.selectedTwootType !== 'draft'){
        state.users.twoots.unshift({
          id: state.users.twoots.length + 1,
          content: state.newTwootContent
        })
        state.newTwootContent ="";

      }
    }

    return {
      state,
      newTwootCharacterCount,
      followUser,
      togglefavourite,
      createNewTwoot,
      userId
    }

  }




}
</script>

<style  scoped>

.user-profile{
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;
}

.user-profile__user-panel{
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: white;
  border-right: 5px;
  border: 1px solid #DFE3E8;
}
h1{
  margin: 0;
}

.user-profile__admin-bagde{
  background-color: rebeccapurple;
  color:white;
  margin-right: auto;
  border-radius: 5px;
  padding:0 10px;
  font-weight: bold;
}
.user-profile__twoots-wrapper{
  display: grid;
  grid-gap: 10px;
}
.user-profile__create-twoot {
  display: flex;
  flex-direction: column;
  padding: 20px;
  border: 1px solid #DFE3E8;

}
.--exceeded{
  color:red;
  border-color: red;
}

button {
  background-color: red;
  color: white;
}
</style>
