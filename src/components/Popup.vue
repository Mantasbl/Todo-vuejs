<template>
    <v-dialog max-width="600px">
        <template v-slot:activator="{ on }">
            <v-btn depressed color="#fafafa" class="success" v-on="on">
                Add new project
            </v-btn>
        </template>
        <v-card>
            <v-card-title>
                <h2>Add a New project</h2>
            </v-card-title>
        </v-card>
    </v-dialog>
</template>

<script>
export default {
    
}
</script>