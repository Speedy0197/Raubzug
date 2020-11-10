<template>
  <v-container @keyup.enter="submit()">
    <v-card>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field
                label="Speere"
                type="number"
                v-model="form.speere"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="Schwerter"
                type="number"
                v-model="form.schwerter"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="Äxte"
                type="number"
                v-model="form.axt"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="Lkav"
                type="number"
                v-model="form.lkav"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="Skav"
                type="number"
                v-model="form.skav"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="submit"> Berechnen </v-btn>
        <v-spacer></v-spacer>
      </v-card-actions>
    </v-card>
    <br />
    <v-data-table
      v-if="info"
      :headers="headers"
      :items="items"
      :hide-default-footer="true"
    ></v-data-table>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      form: {
        speere: 0,
        schwerter: 0,
        axt: 0,
        lkav: 0,
        skav: 0,
      },
      headers: [
        { text: "Stufe", value: "stufe", sortable: false },
        { text: "Speere", value: "speere", sortable: false },
        { text: "Schwerter", value: "schwerter", sortable: false },
        { text: "Äxte", value: "axt", sortable: false },
        { text: "Lkav", value: "lkav", sortable: false },
        { text: "Skav", value: "skav", sortable: false },
      ],
      items: [],
      info: false,
    };
  },
  methods: {
    submit() {
      if (!this.form.speere) {
        this.form.speere = 0;
      }
      if (!this.form.schwerter) {
        this.form.schwerter = 0;
      }
      if (!this.form.axt) {
        this.form.axt = 0;
      }
      if (!this.form.lkav) {
        this.form.lkav = 0;
      }
      if (!this.form.skav) {
        this.form.skav = 0;
      }

      this.items = [];
      let maxkap =
        this.form.speere * 25 +
        this.form.schwerter * 15 +
        this.form.axt * 10 +
        this.form.lkav * 80 +
        this.form.skav * 50;
      let a1 = 0;
      let a2 = 0;
      let a3 = 0;
      let end = 0;

      for (let x1 = 0; x1 < 101; x1++) {
        for (let x2 = 0; x2 < 101; x2++) {
          for (let x3 = 0; x3 < 101; x3++) {
            if (x1 + x2 + x3 == 100) {
              let loot1 = (maxkap * x1 * 0.1) / 100;
              let loot2 = (maxkap * x2 * 0.25) / 100;
              let loot3 = (maxkap * x3 * 0.5) / 100;
              let wert1 = 0;
              let wert2 = 0;
              let wert3 = 0;

              if (loot1 != 0) {
                let testloot1 = Math.pow(loot1, 2) * 100;
                let test2loot1 = Math.pow(testloot1, 0.45);
                let test3loot1 = (test2loot1 + 1800) * 0.8845033719;
                wert1 = loot1 * ((24 * 60 * 60 * 7) / test3loot1);
              }
              if (loot2 != 0) {
                let testloot2 = Math.pow(loot2, 2) * 100;
                let test2loot2 = Math.pow(testloot2, 0.45);
                let test3loot2 = (test2loot2 + 1800) * 0.8845033719;
                wert2 = loot2 * ((24 * 60 * 60 * 7) / test3loot2);
              }
              if (loot3 != 0) {
                let testloot3 = Math.pow(loot3, 2) * 100;
                let test2loot3 = Math.pow(testloot3, 0.45);
                let test3loot3 = (test2loot3 + 1800) * 0.8845033719;
                wert3 = loot3 * ((24 * 60 * 60 * 7) / test3loot3);
              }
              let temp1 = {
                speere: (this.form.speere * x1) / 100,
                schwerter: (this.form.schwerter * x1) / 100,
                axt: (this.form.axt * x1) / 100,
                lkav: (this.form.lkav * x1) / 100,
                skav: (this.form.skav * x1) / 100,
              };
              let temp2 = {
                speere: (this.form.speere * x2) / 100,
                schwerter: (this.form.schwerter * x2) / 100,
                axt: (this.form.axt * x2) / 100,
                lkav: (this.form.lkav * x2) / 100,
                skav: (this.form.skav * x2) / 100,
              };
              let temp12 =
                temp1.speere +
                temp1.schwerter +
                temp1.axt +
                temp1.lkav +
                temp1.skav;
              if (temp12 < 10) {
                wert1 = 0;
              }
              let temp22 =
                temp2.speere +
                temp2.schwerter +
                temp2.axt +
                temp2.lkav +
                temp2.skav;
              if (temp22 < 10) {
                wert2 = 0;
              }
              let gesamtwert = wert1 + wert2 + wert3;
              if (gesamtwert >= end && x3 > x2 && x2 > x1) {
                end = gesamtwert;
                a1 = x1;
                a2 = x2;
                a3 = x3;
              }
            }
          }
        }
      }

      let end1 = {
        stufe: "Stufe 1",
        speere: Math.round((this.form.speere * a1) / 100),
        schwerter: Math.round((this.form.schwerter * a1) / 100),
        axt: Math.round((this.form.axt * a1) / 100),
        lkav: Math.round((this.form.lkav * a1) / 100),
        skav: Math.round((this.form.skav * a1) / 100),
      };

      let end2 = {
        stufe: "Stufe 2",
        speere: Math.round((this.form.speere * a2) / 100),
        schwerter: Math.round((this.form.schwerter * a2) / 100),
        axt: Math.round((this.form.axt * a2) / 100),
        lkav: Math.round((this.form.lkav * a2) / 100),
        skav: Math.round((this.form.skav * a2) / 100),
      };

      let end3 = {
        stufe: "Stufe 3",
        speere: Math.round((this.form.speere * a3) / 100),
        schwerter: Math.round((this.form.schwerter * a3) / 100),
        axt: Math.round((this.form.axt * a3) / 100),
        lkav: Math.round((this.form.lkav * a3) / 100),
        skav: Math.round((this.form.skav * a3) / 100),
      };

      this.items.push(end1);
      this.items.push(end2);
      this.items.push(end3);
      this.info = true;
    },
  },
};
</script>
