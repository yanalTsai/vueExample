<template>
 
 <div>
 <v-app>
			<v-content>
      
     <v-layout row wrap>
    <v-flex xs2>
    <side-bar :messages="messages"></side-bar>
    </v-flex>
    <v-flex>
    <v-layout>
    <v-flex >
    <app-content :messages="messages"></app-content>
     </v-flex>
    </v-layout>
    </v-flex>
    </v-layout>
      
			</v-content>
		</v-app>
     <div>
   
</div>
 </div>
</template>

<script>
import sideBar from './sidebar.vue'
import content from './content.vue'
import Msgs from './assets/messages.js'
export default {
  data(){
    return{
      messages:Msgs
    }
  },
components:{
sideBar:sideBar,
appContent:content
}
}
</script>
