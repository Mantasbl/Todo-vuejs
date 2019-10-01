<template>
  <div class="dashboard">
    <v-subheader class="grey--text">Dashboard</v-subheader>

    <v-container class=" my-5">

        <v-row class="mb-3 ml-3">
          <v-tooltip top>
            <template v-slot:activator="{ on }">
              <v-btn small depressed color="#fafafa" class="grey--text" @click="sortBy('title')" v-on="on">
                <v-icon left small>mdi-folder</v-icon>
                <span class="caption text-lowercase">By project name</span>
              </v-btn>
            </template>
            <span>Sort projects by project name</span>
          </v-tooltip>
          <v-tooltip top>
            <template v-slot:activator="{ on }">
              <v-btn small depressed color="#fafafa" class="grey--text" @click="sortBy('person')" v-on="on">
                <v-icon left small>mdi-account</v-icon>
                <span class="caption text-lowercase">By person</span>
              </v-btn>
            </template>
            <span>Sort projects by person</span>
          </v-tooltip>
        </v-row>

        <v-card flat class="mx-4" v-for="project in projects" :key="project.title">
          <v-row :class="`pa-3 project ${project.status}`">
             <v-col cols="12" md="6">
               <div class="caption grey--text">Project title</div>
               <div>{{project.title}}</div>
             </v-col>
             <v-col cols="6" sm="4" md="2">
               <div class="caption grey--text">Person</div>
               <div>{{project.person}}</div>
             </v-col>
             <v-col cols="6" sm="4" md="2">
               <div class="caption grey--text">Due by</div>
               <div>{{project.due}}</div>
             </v-col>
             <v-col cols="4" sm="4" md="2">
               <div class="text-right pr-12">
                 <v-chip :class="`${project.status} white--text caption my-2 v-chip-active`">
                   {{project.status}}
                 </v-chip>
               </div>
             </v-col>
          </v-row>
          <v-divider></v-divider>
        </v-card>
    </v-container>
  </div>
</template>

<script>
import db from '../fb'

export default {
  data() {
    return {
      projects: []
    }
  },
  methods: {
    sortBy(prop) {
      this.projects.sort((a,b) => a[prop] < b [prop] ? -1 : 1)
    } 
  },
  created() {
    db.collection('projects').onSnapshot(res => {
      const changes = res.docChanges()

      changes.forEach(change => {
        if (change.type === 'added'){
          this.projects.push({
            ...change.doc.data(),
            id: change.doc.id
          })
        }
      })
    })
  }
};
</script>

<style>
  .v-card{
    word-break:normal;
  }
  .project.complete {
    border-left: 4px solid #3cd1c2;
  }
  .project.ongoing {
    border-left: 4px solid orange;
  }
  .project.overdue {
    border-left: 4px solid tomato;
  }
  .v-chip.complete.v-chip:not(.v-chip--active) {
    background: #3cd1c2;
  }
  .v-chip.ongoing.v-chip:not(.v-chip--active) {
    background: orange;
  }
  .v-chip.overdue.v-chip:not(.v-chip--active) {
    background: tomato;
  }
</style>