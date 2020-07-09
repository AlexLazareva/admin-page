<template>
  <!-- Текстовое поле -->
  <v-row v-if="type === 'string'">
    <v-text-field
            v-model="name"
            :label="label"
            :rules="rules"
    ></v-text-field>
  </v-row>
  <!-- Текстовое поле END -->
  <!-- Выпадающий список -->
  <v-row v-else-if="type === 'select'">
    <v-select
            v-model="gender"
            :items="meta.values"
            item-value="value"
            item-text="label"
            :label="label"
            dense
    ></v-select>
  </v-row>
  <!-- Выпадающий список END -->
  <!-- Поле даты -->
  <v-row v-else-if="type === 'date'">
    <div class="field text__field">
      <v-menu
              ref="startMenu"
              v-model="startMenu"
              :close-on-content-click="false"
              :nudge-right="40"
              :return-value.sync="start"
              transition="scale-transition"
              min-width="290px"
              offset-y
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
                  v-model="start"
                  class="mt-3"
                  :label="label"
                  dense
                  outlined
                  hide-details
                  v-bind="attrs"
                  v-on="on"
          ></v-text-field>
        </template>
        <!-- Календарь -->
        <v-date-picker
                v-model="start"
                no-title
                scrollable
        >
          <v-spacer></v-spacer>
          <!-- Кнопки календаря -->
          <v-btn
                  text
                  color="primary"
                  @click="$refs.startMenu.save(start)"
          >
            OK
          </v-btn>
          <v-btn
                  text
                  color="primary"
                  @click="startMenu = false"
          >
            Cancel
          </v-btn>
          <!-- Кнопки календаря END -->
        </v-date-picker>
        <!-- Календарь END -->
      </v-menu>
    </div>
  </v-row>
  <!-- Поле даты END -->
</template>

<script>
export default {
  name: 'UserForm',
  props: {
    label: String,
    type: String,
    meta: Object,
    validator: Function
  },
  data: () => ({
    name: null,
    gender: null,
    startMenu: false,
    start: '2019-01-12',
    events: [],
    items: [],
    rules: [
            value => !!value || 'Required'
    ]
  }),
  methods: {
    getEvents ({ start, end }) {
      const events = [];

      const min = new Date(`${start.date}T00:00:00`);
      const max = new Date(`${end.date}T23:59:59`);
      const days = (max.getTime() - min.getTime()) / 86400000;
      const eventCount = this.rnd(days, days + 20);

      for (let i = 0; i < eventCount; i++) {
        const allDay = this.rnd(0, 3) === 0;
        const firstTimestamp = this.rnd(min.getTime(), max.getTime());
        const first = new Date(firstTimestamp - (firstTimestamp % 900000));

        events.push({
          name: this.names[this.rnd(0, this.names.length - 1)],
          start: first,
          timed: !allDay,
          color: this.colors[this.rnd(0, this.colors.length - 1)],
        })
      }

      this.events = events;
    },
    rnd (a, b) {
      return Math.floor((b - a + 1) * Math.random()) + a;
    },
  }
}
</script>

<style lang="scss">

</style>
