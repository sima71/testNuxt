<template>
  <v-app>
    <v-navigation-drawer
      dark
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      right
      dir="rtl"
      width="180"
    >
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
        style="margin-bottom: 30px; margin-top: 25px"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? "right" : "left"}` }}</v-icon>
      </v-btn>

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
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app style="direction: rtl">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <v-btn icon @click.stop="fixed = !fixed"> </v-btn>

      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer"> </v-btn>
    </v-app-bar>

    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>

    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import Logo from "../components/Logo.vue";
export default {
  components: { Logo },
  data() {
    return {
      clipped: false,
      drawer: false,
      right: true,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "صفحه ی اصلی ",

          to: "/",
        },
        {
          icon: " mdi-domain",
          title: "محصولات",
          to: "/mahsulat",
        },
        {
          icon: "mdi-chart-bubble",
          title: "مشتریان",
          to: "/moshtari",
        },
        {
          icon: " mdi-dialpad",
          title: "فروشندگان",
          to: "/forushande",
        },
        {
          icon: "mdi-message-text",
          title: "سفارشات",
          to: "/sefareshat",
        },
        {
          icon: " mdi-wrench",
          title: "تنظیمات",
          to: "/siting",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: true,
      title: "ننننن",
    };
  },
};
</script>
