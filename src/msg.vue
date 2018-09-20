<template>
<v-card>
        <v-img
          class="white--text"
          height="200px"
          src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
        >
          <v-container fill-height fluid>
            <v-layout fill-height>
              <v-flex xs12 align-end flexbox>
                <span class="headline">{{data.subject}}</span>
              </v-flex>
            </v-layout>
          </v-container>
        </v-img>
        <v-card-title>
          <div>
            <span class="grey--text">  {{ data.date.fromNow()}}</span><br>
            <span>From {{data.from.email}}</span><br>
            <span  v-html="data.content"></span>
          </div>
        </v-card-title>
        <v-card-actions>
          <v-btn flat color="orange" @click.stop="data.isRead=!data.isRead">{{(data.isRead)?"Mark as unread":"mark as Read"}}</v-btn>
          <v-btn flat color="orange" @click.prevent.stop="Del">Delete</v-btn>
        </v-card-actions>
      </v-card>
</template>
<script>
export default {
  activated(){
    this.data.isRead=true;
  },
   props: {
    data: {
      type: Object,
      required: true
    }
  },
   data: () => ({
      show: false
    }),
    methods:{
      Del:function(){
        this.data.isDeleted=true;

      }
    }
};
</script>
