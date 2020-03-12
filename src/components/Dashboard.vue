<template>
  <v-container>
    <v-row>
      <v-col cols="8">
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
      <v-col>
        <v-container>
          <v-row>
            <v-col cols="12" v-for="(tf, i) in tagFilter" :key="i">
              <draggable
                :list="tf.tags"
                group="filterColumn"
                class="filterContainer"
                v-bind:class="tf.tags.length == 0 ? 'lowOpacity' : ''"
                ghostClass="ghost"
                @start="dragActive = true"
                @end="dragActive = false"
              >
                <v-chip v-for="(tag, j) in tf.tags" :key="j">{{ tag }}</v-chip>
              </draggable>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "Dashboard",
  components: {
    draggable
  },
  data: function() {
  return {
      dragActive: false,
      abonnements: [
        {
          name: "Netflix",
          price: 10.0,
          interval: "monthly"
        },
        {
          name: "Spotify",
          price: 10.0,
          interval: "monthly"
        },
        {
          name: "VPN Express",
          price: 12.0,
          interval: "monthly"
        }
      ],
      tagFilter: [
        { tags: ["expense", "income", "sanitary", "party", "food"] },
        { tags: [] }
      ]
    };
  },
  methods: {
    dragEnded: event => {
      console.log(event);
    }
  },
  watch:{
    dragActive: function(val) {
      if (val == false) {
        console.log("drag ended")
        if (this.tagFilter[this.tagFilter.length - 1].lenth > 0) {
          this.tagFilter.push({ tags: [] });
        }
      }
    }
  }
};
</script>

<style scoped>
.fCards {
  margin-bottom: 10px;
}

.filterContainer {
  min-width: 30px;
  min-height: 80px;
  background-color: bisque;
  opacity: 0.7;
}

.flip-list-move {
  transition: transform 0.5s;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-active {
  transition-delay: 0.2s;
}
.lowOpacity {
  opacity: 0.5 !important;
}
</style>