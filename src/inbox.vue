<template>
  <app-msgs :messages="iMessages"></app-msgs>
</template>
<script>
import msgs from "./msgs.vue";
export default {
  components: {
    appMsgs: msgs
  },
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  computed: {
    iMessages() {
      return this.data.messages.filter(function(msg) {
        return msg.type == "incoming" && !msg.isDeleted;
      });
    }
  }
};
</script>
