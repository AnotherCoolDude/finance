<template>
    <v-container>
          <v-row>
            <draggable
              :list="tagFilter"
              class="filterContainer"
              ghostClass="ghost"
              :move="onMove"
            >
            <v-col cols="12" v-for="(tf, i) in tagFilter" :key="i">
              <draggable
                :list="tf.tags"
                group="filterColumn"
                class="tagContainer"
                v-bind:class="tf.tags.length == 0? 'noOpacity' : ''"
                ghostClass="ghost"
                @start="onStart"
                @end="onEnd"
                :move="onMove"
              >
                <v-chip v-for="(tag, j) in tf.tags" :key="j">{{ tag }}</v-chip>
              </draggable>
            </v-col>
            </draggable>
          </v-row>
        </v-container>
</template>