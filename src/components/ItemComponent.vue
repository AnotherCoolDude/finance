<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <draggable v-model="abonnements">
          <v-card v-for="(abo, i) in abonnements" :key="i" class="fCards">
            <v-card-title>
              <span class="title font-weight-light">{{ abo.name }}</span>
            </v-card-title>
            <v-card-text>
              <span>costs you {{ abo.price }}€ {{ abo.interval }}</span>
            </v-card-text>
          </v-card>
        </draggable>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    props: {
        items: {
            name: String,
            price: Number,
            interval: String
        }
    }
})
</script>