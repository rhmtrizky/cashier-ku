<template>
  <v-app dark>
    <v-navigation-drawer v-model="sideDrawer" :mini-variant="miniVariant" app>
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <!-- <v-app-bar :clipped-left="clipped" fixed app>
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? "right" : "left"}` }}</v-icon>
      </v-btn>
    </v-app-bar> -->
    <v-main>
      <v-container fluid>
        <Nuxt />
      </v-container>
    </v-main>
    <v-bottom-navigation horizontal fixed app>
      <v-app-bar-nav-icon
        @click.stop="sideDrawer = !sideDrawer"
        v-ripple="false"
        plain
      />
      <v-btn
        v-for="(item, i) in bottomMenu"
        :key="i"
        :to="item.to"
        v-ripple="false"
        plain
      >
        <span>{{ item.title }}</span>
        <v-icon>{{ item.icon }}</v-icon>
      </v-btn>
      <v-spacer />
    </v-bottom-navigation>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      sideDrawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-account",
          title: "Account",
          to: "/account",
        },
        {
          icon: "mdi-bell",
          title: "Notification",
          to: "/notification",
        },
      ],
      bottomMenu: [
        {
          icon: "mdi-application",
          title: "App",
          to: "/",
        },
      ],
      miniVariant: false,
    };
  },
};
</script>
