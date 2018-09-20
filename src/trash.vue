<template>
 <app-msgs :messages="trashedMessages"></app-msgs>
</template>
<script>
import Msgs from "./msgs.vue"
export default {
  components: {
    appMsgs: Msgs
  },
  props:{
    data:{
      type:Object,
      required:true
    }
  },
  computed:{
    trashedMessages() {
      return this.data.messages.filter(function(message) {
        return message.isDeleted === true;
      })
    }
  }
  };
</script>
