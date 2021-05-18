<template>
<div class="container">
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="text-center">
        <div style="margin-left: -279px">
          <v-sheet tile height="54" class="d-flex" width="330">
            <v-btn icon  @click="$refs.calendar.prev()"  width=10> 
              <v-icon>mdi-chevron-left</v-icon>
            </v-btn>
            <v-select
              v-model="type"
              :items="types"
              dense
              outlined
              hide-details
            
              label="type"
            ></v-select>
            <v-select
              v-model="mode"
              :items="modes"
              dense
              outlined
              hide-details
              label="event-overlap-mode"
         
            ></v-select>
            <v-select
              v-model="weekday"
              :items="weekdays"
              dense
              outlined
              hide-details
              label="weekdays"
            
            ></v-select>
            <v-spacer></v-spacer>
            <v-btn icon  @click="$refs.calendar.next()" width=10>
              <v-icon>mdi-chevron-right</v-icon>
            </v-btn>
          </v-sheet>
          <v-sheet height="294 " width="330">
            <v-calendar
              ref="calendar"
              v-model="value"
              :weekdays="weekday"
              :type="type"
              :events="events"
              :event-overlap-mode="mode"
              :event-overlap-threshold="30"
              :event-color="getEventColor"
              @change="getEvents"
            ></v-calendar>
          </v-sheet>
        </div>
        <div>
          <div
            style="
              border: 1px solid blue;
              width: 761px;
              height: 107px;
              margin-left: 80px;
              margin-top: -333px;
            "
          ></div>
          <div
            style="
              border: 1px solid red;
              width:761px;
              height: 364px;
              margin-left: 80px;
              margin-top: 10px;
            "
          ></div>
          <div>
            <div
              style="
                border: 1px solid black;
                width:337px;
                height: 73px;
                margin-top: -120px;
                margin-left: -284px;
              "
            ></div>
            <div
              style="
                border: 1px solid black;
                width: 337px;
                height: 73px;
                margin-top: 15px;
                margin-left: -284px;
              "
            ></div>
            <div
              style="
                border: 1px solid black;
                width:337px;
                height: 73px;
                margin-top: 15px;
                margin-left: -284px;
              "
            ></div>
          </div>
        </div>
        <div
          dir="rtl"
          style="

            width:761px;
            height: 276px;
            margin-left: 80px;
            margin-top: -114px;
          "
        >
          <v-data-table
            dense
            :headers="headers"
            :items="tablle"
            item-key="name"
            class="elevation-1"
          ></v-data-table>
        </div>
        <div>
          <img
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRgddOGQGaQkNaMmwgqZc-Qz0dpSFv2ed0rxmChaZiog7TlufnFOUh1B0UdV0A1Rm5aH94&usqp=CAU"
            alt=""
            style="margin-top: -139px; margin-left: -802px"
          />
        </div>
      </div>
    </v-col>
  </v-row>
</div>
</template>

  
  


<script>
export default {
  data: () => ({
    type: "month",
    types: ["month", "week", "day", "4day"],
    mode: "stack",
    modes: ["stack", "column"],
    weekday: [0, 1, 2, 3, 4, 5, 6],
    weekdays: [
      { text: "Sun - Sat", value: [0, 1, 2, 3, 4, 5, 6] },
      { text: "Mon - Sun", value: [1, 2, 3, 4, 5, 6, 0] },
      { text: "Mon - Fri", value: [1, 2, 3, 4, 5] },
      { text: "Mon, Wed, Fri", value: [1, 3, 5] },
    ],
    value: "",
    events: [],
    colors: [
      "blue",
      "indigo",
      "deep-purple",
      "cyan",
      "green",
      "orange",
      "grey darken-1",
    ],
    names: [
      "Meeting",
      "Holiday",
      "PTO",
      "Travel",
      "Event",
      "Birthday",
      "Conference",
      "Party",
    ],
    tablle: [
      {
        name: "sima sedighi",
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        iron: "1%",
      },
    ],
    headers: [
      {
        text: "نام و نام خانوادگی",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Calories", value: "calories" },
      { text: "Fat (g)", value: "fat" },
      { text: "Carbs (g)", value: "carbs" },
      { text: "Protein (g)", value: "protein" },
      { text: "Iron (%)", value: "iron" },
    ],
  }),
  methods: {
    getEvents({ start, end }) {
      const events = [];

      const min = new Date(`${start.date}T00:00:00`);
      const max = new Date(`${end.date}T23:59:59`);
      const days = (max.getTime() - min.getTime()) / 86400000;
      const eventCount = this.rnd(days, days + 20);

      for (let i = 0; i < eventCount; i++) {
        const allDay = this.rnd(0, 3) === 0;
        const firstTimestamp = this.rnd(min.getTime(), max.getTime());
        const first = new Date(firstTimestamp - (firstTimestamp % 900000));
        const secondTimestamp = this.rnd(2, allDay ? 288 : 8) * 900000;
        const second = new Date(first.getTime() + secondTimestamp);

        events.push({
          name: this.names[this.rnd(0, this.names.length - 1)],
          start: first,
          end: second,
          color: this.colors[this.rnd(0, this.colors.length - 1)],
          timed: !allDay,
        });
      }

      this.events = events;
    },
    getEventColor(event) {
      return event.color;
    },
    rnd(a, b) {
      return Math.floor((b - a + 1) * Math.random()) + a;
    },
  },
};
</script>

