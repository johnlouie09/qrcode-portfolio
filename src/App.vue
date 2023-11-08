<template>
    <v-layout class="rounded rounded-md">
        <v-app-bar :title="title">
            <template v-slot:prepend>
                <v-app-bar-nav-icon @click="drawer = !drawer" :elevation="2" rounded></v-app-bar-nav-icon>
            </template>
            <template v-slot:append>
                <v-switch
                    v-model="isDark"
                    hide-details
                    inset="true"
                    label="Dark Mode"
                    @change="toggleTheme"
                >
                </v-switch>
            </template>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" permanent="true">
            <v-card
                class="mx-auto pa-2"
                max-width="300"
                variant="flat"
            >
                <v-list>
                    <v-list-item
                        v-for="(sidebarItem, sidebarItemIndex) in sidebar.items"
                        :key="sidebarItem.id"
                        :value="sidebarItem"
                        color="primary"
                        rounded="xl"
                        class="my-1"
                        :active="sidebarItem.id === page"
                        @click="page = sidebarItem.id"
                    >
                        <template v-slot:prepend>
                            <v-icon :icon="sidebarItem.icon"></v-icon>
                        </template>

                        <v-list-item-title v-text="sidebarItem.text"></v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-card>
        </v-navigation-drawer>

        <v-main>
            <app-main :page="page" />
        </v-main>
    </v-layout>
</template>


<script>
    import { defineComponent } from 'vue';
    import Main    from "./components/Main.vue";

    export default defineComponent({
        name: 'App',

        /** DATA */
        data() {
            return {
                title : 'Portfolio',
                isDark: true,
                drawer: true,
                page  : 'home',
                sidebar: {
                    items: [
                        { id: 'home'   , text: 'Home'      , icon: 'mdi-home'        },
                        { id: 'about'  , text: 'About'     , icon: 'mdi-information' },
                    ],
                }
            }
        },

        /** COMPONENTS */
        components: {
            'app-main': Main,
        },

        /** METHODS */
        methods: {
            switchMode(mode) {
                if (this.config.use_cookies) {
                    this.$cookie.set("nightMode", mode);
                }
                this.nightMode = mode;
                },
            scrollTo(ele) {
            if (ele == "home") {
                this.$router.push(`/`);
                window.scrollTo({ top: -80, behavior: "smooth" });
            } else {
                var elementPosition = document.getElementById(ele).offsetTop;
                window.scrollTo({ top: elementPosition - 35, behavior: "smooth" });
                if (this.$router.history.current.path !== `/${ele}`)
                this.$router.push(`/${ele}`);
            }
            },
            toggleTheme() {
                this.$vuetify.theme.global.name = this.isDark ? 'dark' : 'light';
            }
        },

        computed: {
            scrollbarTheme() {
            return this.$vuetify.theme.dark ? 'dark' : 'light';
            }
        }
    });
</script>


<style>
/* To set scrollbar width */
::-webkit-scrollbar {
  width: 5px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 9px;
  border: 2px solid white; /* Use your background color instead of White */
  background-clip: content-box;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 9px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
