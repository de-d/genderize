<template>
  <v-app theme="dark">
    <v-main>
      <v-container class="fill-height" fluid>
        <v-row justify="center" align="center">
          <v-col md="3">
            <Genderize />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup lang="ts">
import Genderize from './components/Genderize.vue';
</script>