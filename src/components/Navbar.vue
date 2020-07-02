<template>  
    <nav>
        <v-toolbar app dark>
            <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
            <span>IoT Dashboard</span>
        </v-toolbar>

        <v-spacer></v-spacer>

        <v-navigation-drawer app v-model="drawer" dark color="blue">
            <v-list>
                <v-list-item
                v-for="item in items"
                :key="item.title"
                >
                <v-list-item-icon>
                    <v-icon>{{ item.icon }} </v-icon>
                </v-list-item-icon>

                <v-list-item-content>
                    <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item-content>

                </v-list-item>
            </v-list>

        </v-navigation-drawer>
        
    </nav>
</template>

<script>
export default {
    data() {
        return {
            drawer:false,
            items:[
                { title: 'Dashboard',  icon: 'mdi-home' },
                { title: 'Smart Plug', icon: 'mdi-home' },
                { title: 'Smart Fan',  icon: 'mdi-fan'  },
                { title: 'Settings',  icon: 'mdi-settings'},
            ]
        }
    },

}
</script>

<style>

</style>