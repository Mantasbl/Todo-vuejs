<template>
    <nav>
        <v-app-bar app flat color="#fafafa">
            <v-app-bar-nav-icon @click="drawer = !drawer" ></v-app-bar-nav-icon>
            <v-toolbar-title class="text-uppercase grey--text">
                <span class="font-weight-light">Todo</span>
                <span>list</span>
            </v-toolbar-title>
            <v-spacer></v-spacer> 

            <v-menu offset-y>
                <template v-slot:activator="{ on }">
                    <v-btn depressed color="#fafafa" v-on="on">
                        <v-icon left>mdi-chevron-down</v-icon>
                        <span>Menu</span>
                    </v-btn>
                </template>
                <v-list>
                    <v-list-item v-for="link in links" 
                        :key="link.text"
                        route :to="link.route">
                        <v-list-item-title>
                            {{link.text}}
                        </v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>

            <v-btn depressed color="#fafafa">
                <span>Sign Out</span>
                <v-icon right>mdi-exit-to-app</v-icon>
            </v-btn>
        </v-app-bar>

        <v-navigation-drawer app v-model="drawer" class="primary">
            <v-row >
                <v-col class="mt-5" align="center">
                    <v-avatar size="100">
                        <img src="/avatar-1.png">
                    </v-avatar>
                    <p class="white--text subheading mt-3">
                        BaltakisDev
                    </p>
                </v-col>
                <v-col align="center" class="mt-2 mb-3">
                    <Popup/>
                </v-col>
            </v-row>
            <v-list>
                <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
                    <v-list-item-icon>
                        <v-icon class="white--text">{{ link.icon }}</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                        <v-list-item-title class="white--text">{{ link.text }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
    </nav>
</template>

<script>
import Popup from './Popup'
export default {
    components: {
        Popup
    },
    data() {
        return {
            drawer: true,
            links: [
                { icon: 'mdi-view-dashboard', text: 'Dashboard', route: '/' },
                { icon: 'mdi-folder', text: 'My Projects', route: '/projects' },
                { icon: 'mdi-account', text: 'Team', route: '/team' },
            ]
        }
    }
}
</script>

<style>

</style>