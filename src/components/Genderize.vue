<script setup lang="ts">
  import { ref } from 'vue'

  const name = ref("")
  const genderName = ref("")
  const genderResult = ref("")
  const isVisible = ref(false)

  async function Gen() {
    const url = "https://api.genderize.io/?name=" + name.value

    const response = fetch(url)

    if ((await response).ok) {
      const data = await (await response).json()
      genderResult.value = data.gender
      genderName.value = data.name
      if (genderResult.value !== "male" && genderResult.value !== "female") {
        genderResult.value = "Unknown"
      }
    } else {
      throw new Error("Network response was not ok.")
    }

    if (genderResult.value !== "") {
      isVisible.value = true
    } else {
      isVisible.value = false
    }
  }

</script>

<template>
  <v-card class="card">
    <v-card-title class="card-title">
      <span class="text-h5">Genderize</span>
      <v-icon icon="mdi-gender-male-female" color="green"></v-icon>
    </v-card-title>
     <v-card-text>
      <v-text-field
        class="no-hint"
        density="compact"
        variant="outlined"
        label="Имя"
        autocomplete="new-password"
        append-inner-icon="mdi-magnify"
        v-model="name"
        @click:append-inner="Gen">
      </v-text-field>
    </v-card-text>
      <v-btn v-if="isVisible" class="gender-result" variant="tonal" color="green">
        {{ genderName }} - {{ genderResult }}
      </v-btn>
  </v-card>
</template>

<style scoped>
  .card {
    display: flex;
    flex-direction: column;
    align-self: flex-end;
    max-width: 400px;
    background-color: #1f2f34;
    padding: 35px;
  }
  .card-title {
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
  .gender-result {
    margin: 0 auto;
  }
</style>


