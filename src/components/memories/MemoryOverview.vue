<template>
  <ion-img :src="image" :alt="title"></ion-img>
  <h2 class="ion-text-center">{{ title.toUpperCase() }}</h2>
  <hr />
  <p class="ion-text-center">{{ description }}</p>
</template>

<script>
import { IonImg } from "@ionic/vue"

export default {
  props: ["title", "image", "description"],
  components: {
    IonImg,
  },
}
</script>

<style scoped>
hr {
  background-color: rgb(241, 241, 241);
  height: 2px;
  margin: 1rem;
}

p {
  margin: 0 0.8rem;
  font-size: 1.3rem;
}
</style>