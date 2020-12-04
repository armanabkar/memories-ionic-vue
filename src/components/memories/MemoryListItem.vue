<template>
  <ion-item :router-link="`/memories/${memory.id}`">
    <ion-thumbnail slot="start">
      <ion-img :src="memory.image" :alt="memory.title"></ion-img>
    </ion-thumbnail>
    <ion-label>
      {{ memory.title.toUpperCase() }}
    </ion-label>
  </ion-item>
</template>

<script>
import { IonItem, IonThumbnail, IonImg, IonLabel } from "@ionic/vue"

export default {
  props: ["memory"],
  components: {
    IonItem,
    IonThumbnail,
    IonImg,
    IonLabel,
  },
}
</script>

<style scoped>
ion-label {
  font-weight: bold;
}

ion-img {
  border-radius: 4px;
}

ion-item {
  margin-right: 1.5rem;
}
</style>