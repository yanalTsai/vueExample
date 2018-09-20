<template>
 <app-msgs :messages="sentMges"></app-msgs>
</template>
<script>
import Msgs from './msgs.vue'
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
    sentMges() {
      return this.data.messages.filter(function(message) {
        return message.type == "outgoing" && !message.isDeleted;
      });
    }
  }
};
</script>
