<template>
  <div class="projects">
    <v-subheader class="grey--text">Projects</v-subheader>

    <v-container class=" my-5">
        <v-expansion-panels>
          <v-expansion-panel v-for="project in myProjects" :key="project.title">
            <v-expansion-panel-header>
              {{project.title}}
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              <v-card flat>
                <v-card-text>
                  <div class="font-weight-bold">Due by {{project.due}}</div>
                  <div>{{project.content}}</div>
                </v-card-text>
              </v-card>
            </v-expansion-panel-content>
          </v-expansion-panel>
        </v-expansion-panels>
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
  computed: {
    myProjects() {
      return this.projects.filter(project => {
        return project.person === 'BaltakisDev'
      })
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
