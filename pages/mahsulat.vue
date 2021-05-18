

<template>
  <v-card dir="rtl">
    <v-toolbar>
      <v-toolbar-title>محصولات</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      <v-toolbar-title>جستجو</v-toolbar-title>

      <template v-slot:extension>
        <v-tabs v-model="tab" align-with-title>
          <v-tabs-slider color="yellow"></v-tabs-slider>

          <v-tab href="#tab-1"> همه ی محصولات </v-tab>

          <v-tab href="#tab-2"> ایجاد محصول fffffff جدید </v-tab>
        </v-tabs>
      </template>
    </v-toolbar>

    <v-tabs-items v-model="tab">
      <v-tab-item id="tab-1">
        <v-card style="margin-top: 30px; margin-bottom: 70px">
          <v-card-title>
            جستجو برghhhhh اساس
            <v-spacer></v-spacer>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
        </v-card>
        <div>
          <v-data-table
            :headers="headers"
            :items="desserts"
            class="elevation-1"
          >
            <template v-slot:top>
              <v-toolbar flat>
                <v-toolbar-title>لیست محصولات</v-toolbar-title>

                <v-divider class="mx-4" inset vertical></v-divider>
                <v-spacer></v-spacer>
                <v-dialog v-model="dialog" max-width="500px">
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      color="primary"
                      dark
                      class="mb-2"
                      v-bind="attrs"
                      v-on="on"
                    >
                      New Item
                    </v-btn>
                  </template>

                  <v-card>
                    <v-card-title>
                      <span class="headline">{{ formTitle }}</span>
                    </v-card-title>

                    <v-card-text>
                      <v-container>
                        <v-row>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="editedItem.name"
                              label="نام کالا"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="editedItem.calories"
                              label="نام برند "
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="editedItem.fat"
                              label="نام مدل"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="editedItem.carbs"
                              label="عکس محصول"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="editedItem.proteinn"
                              label="قیمت خرید"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="editedItem.protein"
                              label="قیمت فروش"
                            ></v-text-field>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-card-text>

                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="close">
                        Cancel
                      </v-btn>
                      <v-btn color="blue darken-1" text @click="save">
                        Save
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
                <v-dialog v-model="dialogDelete" max-width="500px">
                  <v-card>
                    <v-card-title class="headline"
                      >Are you sure you want to delete this item?</v-card-title
                    >
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="closeDelete"
                        >Cancel</v-btn
                      >
                      <v-btn
                        color="blue darken-1"
                        text
                        @click="deleteItemConfirm"
                        >OK</v-btn
                      >
                      <v-spacer></v-spacer>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </v-toolbar>
            </template>

            <template v-slot:item.actions="{ item }">
              <v-icon small class="mr-2" @click="editItem(item)">
                mdi-pencil
              </v-icon>
              <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
            </template>
            <template v-slot:no-data>
              <v-btn color="primary" @click="initialize"> Reset </v-btn>
            </template>
          </v-data-table>
        </div>
      </v-tab-item>

      <v-tab-item id="tab-2">
        <v-card flat>
          <v-card-text>
            <v-container fluid>
              <v-row align="center">
                <div class="row" style="margin-right: 780px; margin-top: 34px">
                  <v-btn class="ma-2" color="success">
                    ذخیره کردن اطلاعات
                  </v-btn>
                  <v-btn class="ma-2" color="error"> ریسیت کردن </v-btn>
                </div>
                <div class="col-12" style="margin: 40px 0px 25px 0px">
                  <h1>اطلاعات عمومی محصول</h1>
                </div>
                <v-col class="d-flex" cols="12" sm="6">
                  <v-select :items="kala" label="نام کالا" outlined></v-select>
                </v-col>

                <v-col class="d-flex" cols="12" sm="6">
                  <v-select :items="brand" label="نام برند" outlined></v-select>
                </v-col>

                <v-col class="d-flex" cols="12" sm="6">
                  <v-select :items="model" label="نام مدل" outlined></v-select>
                </v-col>

                <v-col class="d-flex" cols="12" sm="6">
                  <v-select :items="vahed" label="واحد" outlined></v-select>
                </v-col>
                <v-divider inset></v-divider>
                <div class="col-12" style="margin: 30px 15px 40px 19px">
                  <h1>عکس محصول</h1>
                </div>

                <v-file-input
                  label="File input"
                  filled
                  prepend-icon="mdi-camera"
                ></v-file-input>

                <v-row>
                  <v-col cols="3" sm="2">
                    <v-img
                      src="https://cdn.vuetifyjs.com/images/parallax/material2.jpg"
                      gradient="to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)"
                    ></v-img>
                  </v-col>

                  <v-col cols="3" sm="2">
                    <v-img
                      src="https://cdn.vuetifyjs.com/images/parallax/material2.jpg"
                    >
                      <div class="fill-height bottom-gradient"></div>
                    </v-img>
                  </v-col>

                  <v-col cols="3" sm="2">
                    <v-img
                      src="https://cdn.vuetifyjs.com/images/parallax/material2.jpg"
                    >
                      <div class="fill-height repeating-gradient"></div>
                    </v-img>
                  </v-col>
                </v-row>

                <v-divider inset style="margin-top: 50px"></v-divider>

                <div class="col-12" style="margin: 30px 15px 40px 19px">
                  <h1>قیمت محصول</h1>
                </div>

                <v-col cols="12" sm="6">
                  <label> قیمت خرید</label>

                  <v-text-field
                    label=" قیمت خرید "
                    single-line
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6">
                  <label> قیمت فروش</label>
                  <v-text-field
                    label="قیمت فروش"
                    single-line
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>

              <div style="margin-top: 55px">
                <v-data-table
                  :headers="headers"
                  :items="desserts"
                  sort-by="calories"
                  class="elevation-1"
                >
                  <template v-slot:top>
                    <v-toolbar flat>
                      <v-toolbar-title>لیست محصولات</v-toolbar-title>
                      <v-divider class="mx-4" inset vertical></v-divider>
                      <v-spacer></v-spacer>
                      <v-dialog v-model="dialog" max-width="500px">
                        <template v-slot:activator="{ on, attrs }">
                          <v-btn
                            color="primary"
                            dark
                            class="mb-2"
                            v-bind="attrs"
                            v-on="on"
                          >
                            New Item
                          </v-btn>
                        </template>
                        <v-card>
                          <v-card-title>
                            <span class="headline">{{ formTitle }}</span>
                          </v-card-title>

                          <v-card-text>
                            <v-container>
                              <v-row>
                                <v-col cols="12" sm="6" md="4">
                                  <v-text-field
                                    v-model="editedItem.name"
                                    label="نام کالا"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12" sm="6" md="4">
                                  <v-text-field
                                    v-model="editedItem.calories"
                                    label="نام برند "
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12" sm="6" md="4">
                                  <v-text-field
                                    v-model="editedItem.fat"
                                    label="نام مدل"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12" sm="6" md="4">
                                  <v-text-field
                                    v-model="editedItem.carbs"
                                    label="عکس محصول"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12" sm="6" md="4">
                                  <v-text-field
                                    v-model="editedItem.proteinn"
                                    label="قیمت خرید"
                                  ></v-text-field>
                                </v-col>
                                <v-col cols="12" sm="6" md="4">
                                  <v-text-field
                                    v-model="editedItem.protein"
                                    label="قیمت فروش"
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                            </v-container>
                          </v-card-text>

                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="blue darken-1" text @click="close">
                              Cancel
                            </v-btn>
                            <v-btn color="blue darken-1" text @click="save">
                              Save
                            </v-btn>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>
                      <v-dialog v-model="dialogDelete" max-width="500px">
                        <v-card>
                          <v-card-title class="headline"
                            >Are you sure you want to delete this
                            item?</v-card-title
                          >
                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn
                              color="blue darken-1"
                              text
                              @click="closeDelete"
                              >Cancel</v-btn
                            >
                            <v-btn
                              color="blue darken-1"
                              text
                              @click="deleteItemConfirm"
                              >OK</v-btn
                            >
                            <v-spacer></v-spacer>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>
                    </v-toolbar>
                  </template>
                  <template v-slot:item.actions="{ item }">
                    <v-icon small class="mr-2" @click="editItem(item)">
                      mdi-pencil
                    </v-icon>
                    <v-icon small @click="deleteItem(item)">
                      mdi-delete
                    </v-icon>
                  </template>
                  <template v-slot:no-data>
                    <v-btn color="primary" @click="initialize"> Reset </v-btn>
                  </template>
                </v-data-table>
              </div>
            </v-container>
          </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      dialogDelete: false,
      tab: null,
      kala: ["ماشین لباس شویی", "ماشین ظرف شویی", "تلوزیون", "کولر گازی"],
      brand: ["الجی", "سامسونگ", "سونی"],
      model: ["Foo", "Bar", "Fizz", "Buzz"],
      vahed: ["Foo", "Bar", "Fizz", "Buzz"],

      headers: [
        {
          text: "نام کالا",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "نام برند ", value: "calories" },
        { text: "نام مدل", value: "fat" },
        { text: "عکس محصول", value: "carbs" },
        { text: "قیمت خرید", value: "protein" },
        { text: "قیمت فروش", value: "proteinn" },
        { text: "Actions", value: "actions", sortable: false },
      ],

      desserts: [],
      editedIndex: -1,
      editedItem: {
        ProdoctName: "",
        NameBrand: 0,
        NameModel: 0,
        prodoctImage: 0,
        kharid: 0,
        forush: 0,
      },
    };
  },

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.desserts = [
        {
          ProdoctName: "Frozen Yogurt",
          NameBrand: "",
          NameModel: 159,
          prodoctImage: 6.0,
          kharid: 24,
          forush: 4.0,
        },
      ];
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.desserts.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
      } else {
        this.desserts.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>

 