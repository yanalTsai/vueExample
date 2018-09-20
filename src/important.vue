
<template>
  <app-msgs :messages="importantMessages"></app-msgs>
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
    importantMessages() {
      return this.data.messages.filter(function(message) {
        return (
          message.type == "incoming" &&
          message.isImportant === true &&
          !message.isDeleted
        );
      });
    }
  }
};
</script>
