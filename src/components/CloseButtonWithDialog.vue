<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" max-width="290">
      <template v-slot:activator="{ on, attrs }">
        <v-btn icon v-bind="attrs" v-on="on">
          <div @click="customOn($event)">
            <v-icon small>mdi-close</v-icon>
          </div>
        </v-btn>
      </template>
      <v-card>
        <v-card-title class="headline">
          タブを消しても大丈夫ですか？
        </v-card-title>
        <v-card-text>編集したデータは失われます。</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="dialog = false">
            消さない
          </v-btn>
          <v-btn color="green darken-1" text @click="$emit('confirmDelete')">
            消す
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  props: {
    tab: Object,
  },
  data() {
    return {
      dialog: false,
    };
  },
  methods: {
    customOn(e) {
      if (!this.tab.modified) {
        this.$emit('confirmDelete');
        e.stopPropagation();
      }
    },
  },
};
</script>