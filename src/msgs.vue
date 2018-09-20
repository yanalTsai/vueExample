<template>
  <v-layout row>
    <v-flex xs12>
      <v-card>
   
        <v-list two-line>
          <template v-for="(message, index) in messages" >
            <v-list-tile   avatar   ripple :key="index" @click.prevent.stop="Move(index)">
              <v-list-tile-content>
                <v-list-tile-title>{{ message.subject }}</v-list-tile-title>
                <v-list-tile-sub-title class="text--primary">{{ message.from.name }}</v-list-tile-sub-title>
                <v-list-tile-sub-title>{{ message.date.fromNow() }}</v-list-tile-sub-title>
              </v-list-tile-content>

              <v-list-tile-action  v-if="message.type !== 'outgoing' " >
                <v-list-tile-action-text></v-list-tile-action-text>
                <v-icon @click.prevent.stop="message.isImportant=!message.isImportant"
                  v-if="!message.isImportant"
                  color="grey lighten-1"
                >
                  star_border
                </v-icon>

                <v-icon @click.prevent.stop="message.isImportant=!message.isImportant"
                  v-else
                  color="yellow darken-2"
                >
                  star
                </v-icon>
              </v-list-tile-action>

            </v-list-tile>
            <v-divider
              v-if="index + 1 < messages.length"
              :key="index"
            ></v-divider>
          </template>
        </v-list>
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>
//import moment from 'moment'
import { eventBus } from "./main.js";
export default {
  props: {
    messages: {
      type: Array,
      required: true
    }
  },

  methods: {
     Move: function(i) {
       eventBus.$emit("move",{ title:this.messages[i].subject , tagName: "app-msg" , data:this.messages[i] })
    
    },
    toggle(index) {
      const i = this.selected.indexOf(index);

      if (i > -1) {
        this.selected.splice(i, 1);
      } else {
        this.selected.push(index);
      }
    }
  }
};
</script>
