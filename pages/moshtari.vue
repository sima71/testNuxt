<template>
  <v-card dir="rtl">
    <v-toolbar
      color="cyan"
      dark
      flat
    >


      <v-toolbar-title>محصولات</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      <v-toolbar-title>جستجو</v-toolbar-title>

    

      <template v-slot:extension>
        <v-tabs
          v-model="tab"
          align-with-title
        >
          <v-tabs-slider color="yellow"></v-tabs-slider>

          <v-tab
            href="#tab-1"
          >
          همه ی محصولات
          </v-tab>
      

         <v-tab
            href="#tab-2"
          >
          ایجاد محصول جدید
          </v-tab>
       </v-tabs>
     
      </template>
    </v-toolbar>

    <v-tabs-items v-model="tab">
      <v-tab-item
       id="tab-1"
      >
        <v-card flat>
          <v-card-text > thisssssssssssssssss</v-card-text>
        </v-card>
      </v-tab-item>

        <v-tab-item
       id="tab-2"
      >
        <v-card flat>
          <v-card-text > fffffffffffffffffffff</v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-card>
</template>

<script>
  export default {
    data () {
      return {
        tab: null,
      }
    },
  }
</script>

