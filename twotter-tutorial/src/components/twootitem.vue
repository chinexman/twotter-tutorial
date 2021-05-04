<template>
  <div class="twoot-item">
     <div class="user-profile__twoot" @click="favouriteTwoot(twoot.id)">
       <div class="twoot-item_user">
         @_{{username}}
       </div>
       <div class="twoot-item__content">
         {{twoot.content}}
       </div>
     </div>
  </div>
</template>

<script>
export default {
  name:"twootitem",
  props: {
   username: {
     type: String,
     required: true
   },
   twoot: {
     type: Object,
     required: true
   }
  },
  methods: {
    favouriteTwoot(id){
      this.$emit('favourite', id)
    }
  }
};
</script>

<style  scoped>
.twoot-item {
  padding: 20px;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;


}
.twoot-item:hover {
  transform: scale(1.1, 1.1);
}
.twoot-item_user {
  font-weight: bold;
}
</style>