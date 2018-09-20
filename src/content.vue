<template>
  <div>
       <v-toolbar color="pink" dark>
        

          <v-toolbar-title>{{currentViwe.title}}</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-btn icon>
            <v-icon>search</v-icon>
          </v-btn>

          <v-btn icon>
            <v-icon>check_circle</v-icon>
          </v-btn>
        </v-toolbar>

  <keep-alive>
  <component :is="currentViwe.tag" :data="currentViwe.data"></component>
  </keep-alive>
  </div>
 
</template>

<script>
import inbox from "./inbox.vue";
import important from "./important.vue";
import msg from "./msg.vue";
import sent from "./sent.vue";
import trash from "./trash.vue";
import { eventBus } from "./main.js";
export default {
  created() {
    eventBus.$on("move", res => {
      let temp = [{ title: res.title, tag: res.tagName, data: res.data || {} }];
      console.log(this.history);
      this.history = temp.concat(this.history.splice(0));
    });
  },
  props: {
    messages: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      history: [
        {
          tag: "app-inbox",
          title: "inbox",
          data: { messages: null }
        }
      ]
    };
  },
  components: {
    appInbox: inbox,
    appMsg: msg,
    appImportant: important,
    appSent: sent,
    appTrash: trash
  },
  computed: {
    currentViwe() {
      let current = this.history[0];
      current.data.messages = this.messages;
      return current;
    }
  }
};
</script>
