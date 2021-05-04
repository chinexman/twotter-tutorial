<template>
  <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot" :class="{'--exceeded':newTwootCharacterCount>180}">
    <label for="newTwoot"><strong>New Twoot:</strong>{{newTwootCharacterCount}}/180</label>
    <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>
    <div class="user-profile__create-type">
      <label for="newTwootType"><strong>Type: </strong></label>
      <select id="newTwootType" v-model="selectedTwootType">
        <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
          {{option.name}}
        </option>
      </select>
    </div>
    <button >
      twoot!
    </button>
  </form>
</template>
<script>
export default {
  name: 'createTwootPanel.vue',
  data () {
    return {
      newTwootContent:"",
      selectedTwootType:'instant',
      twootTypes: [
        { value:'draft', name:"Draft"},
        { value:'instant', name:"Instant Twoot"}
      ],
      followers: 0,
      // oldfollowers:0,
      user: {
        id: 1,
        username: 'chinexman',
        firstname: 'chinedu',
        lastname: 'emordi',
        email: 'chineduemordi@gmail.com',
        userwork:'developer',
        isadmin: true,
        twoots: [
          {
            id: 1,
            content: 'tweeter is amazing'
          },
          {
            id: 2,
            content: 'Dont forget to subscribe to my youtube channerl more light'
          }
        ]
      }
    }
  },
  watch: {
    // followers (oldFollowerCount, newFollowerCount) {
    //   if (oldFollowerCount < newFollowerCount){
    //     console.log(`${this.users.username} has gain afollower`);
    //   }
    // }

    //  if(oldfollowers < followers){
    //    console.log(`${this.users.username} has gain afollower`);
    //
    //  }
  },

  computed: {
    newTwootCharacterCount() {
      return  this.newTwootContent.length;
    }
  },
  methods: {
    followUser () {
      this.oldfollowers = this.followers
      this.followers++
    },


    createNewTwoot() {
      if(this.newTwootContent && this.selectedTwootType !== 'draft'){

        this.$emit('add-twoot', this.newTwootContent);
        // this.user.twoots.unshift({
        //   id: this.user.twoots.length + 1,
        //   content: this.newTwootContent
        // })
        this.newTwootContent ="";

      }
    }

  },

  mounted () {
    this.followUser()
  }

}
</script>

<style  scoped>


h1{
  margin: 0;
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
