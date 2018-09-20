<template>
  <v-card height="100vh">
    <v-navigation-drawer
       
      permanent
      absolute
    >
      <v-toolbar flat class="transparent">
        <v-list class="pa-2">
          <v-list-tile avatar>
            <v-list-tile-avatar>
              <img src="https://randomuser.me/api/portraits/men/85.jpg">
            </v-list-tile-avatar>

            <v-list-tile-content>
              <v-list-tile-title>John Leider</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-toolbar>

      <v-list class="pt-2" dense active> 
        <v-divider></v-divider>

        <v-list-tile
          v-for="item in items"
          :key="item.title"
        @click="navigate(item.title,item.tag)">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>

          <v-list-tile-content>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
            

          </v-list-tile-content>
           <v-list-tile-action>
           <v-badge origin="center" center class="mr-4">
            <span slot="badge" v-if="item.title === 'inbox'">{{unreadMessages.length}}</span>
            <span slot="badge" v-else-if="item.title === 'sent'">{{sentMessages.length}}</span>
            <span slot="badge" v-else-if="item.title === 'important'">{{importantMessages.length}}</span>
            <span slot="badge" v-else-if="item.title === 'trash'">{{trashedMessages.length}}</span>
            </v-badge>
           </v-list-tile-action>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
  </v-card>
</template>
<script>
import { eventBus } from "./main.js";
export default {
  props: {
    messages: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      drawer: true,
      items: [
        { title: "inbox", icon: "dashboard", tag: "app-inbox" },
        { title: "sent", icon: "dashboard", tag: "app-sent" },
        { title: "important", icon: "dashboard", tag: "app-important" },
        { title: "trash", icon: "question_answer", tag: "app-trash" }
      ],
      right: null
    };
  },
  methods: {
    navigate: function(t, tN) {
      eventBus.$emit("move", { title: t, tagName: tN });
    }
  },
  computed: {
    unreadMessages() {
      return this.messages.filter(function(message) {
        return (
          message.type == "incoming" && !message.isRead && !message.isDeleted
        );
      });
    },
    sentMessages() {
      return this.messages.filter(function(message) {
        return message.type == "outgoing" && !message.isDeleted;
      });
    },
    importantMessages() {
      return this.messages.filter(function(message) {
        return (
          message.type == "incoming" &&
          message.isImportant === true &&
          !message.isDeleted
        );
      });
    },
    trashedMessages() {
      return this.messages.filter(function(message) {
        return message.isDeleted === true;
      });
    }
  }
};
</script>
