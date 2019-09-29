<template>
  <div class="team">
    <v-subheader class="grey--text">Team</v-subheader>

    <v-container class=" my-5">
        <v-row>
          <v-col cols="12" sm="6" md="4" lg="3" v-for="person in team" :key="person.name">
            <v-card flat class="text-center">
              <v-responsive class="pt-4">
                <v-avatar size="100" class="grey lighten-2">
                  <img :src="person.avatar">
                </v-avatar>
              </v-responsive>
              <v-card-text>
                <div class="subheading">{{person.name}}</div>
                <div class="grey--text">{{person.role}}</div>
              </v-card-text>
              <v-card-actions>
                <v-btn depressed color="transparent" class="grey--text">
                  <v-icon left>mdi-message-text</v-icon>
                  <span>Message</span>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      team: [
        { name: 'BaltakisDev', role: 'Web developer', avatar:'/avatar-1.png' },
        { name: 'Ryu', role: 'Graphic designer', avatar:'/avatar-2.png' },
        { name: 'Chun Li', role: 'Web developer', avatar:'/avatar-3.png' },
        { name: 'Gouken', role: 'Social media maverick', avatar:'/avatar-4.png' },
        { name: 'Yoshi', role: 'Sales guru', avatar:'/avatar-4.png'}
      ]
    }
  }
};
</script>
