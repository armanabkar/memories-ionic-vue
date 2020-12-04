<template>
  <div>
    <form class="ion-padding" @submit.prevent="submitForm">
      <ion-list>
        <ion-item>
          <ion-label position="floating">Title</ion-label>
          <ion-input type="text" required v-model="enteredTitle" />
        </ion-item>
        <ion-item>
          <ion-label position="floating">Description</ion-label>
          <ion-textarea rows="5" v-model="enteredDescription"></ion-textarea>
        </ion-item>
      </ion-list>
      <img v-if="takenImageUrl" :src="takenImageUrl" />
      <ion-button
        v-if="!takenImageUrl"
        type="button"
        fill="outline"
        @click="takePhoto"
        color="medium"
      >
        <ion-icon slot="start" :icon="camera"></ion-icon>
        Take Photo
      </ion-button>
      <ion-button type="submit" expand="block">Save</ion-button>
    </form>
  </div>
</template>

<script>
import {
  IonList,
  IonItem,
  IonLabel,
  IonInput,
  IonTextarea,
  IonButton,
  IonIcon,
} from "@ionic/vue"
import { camera } from "ionicons/icons"
import { Plugins, CameraResultType, CameraSource } from "@capacitor/core"

const { Camera } = Plugins

export default {
  emits: ["save-memory"],
  components: {
    IonList,
    IonItem,
    IonLabel,
    IonInput,
    IonTextarea,
    IonButton,
    IonIcon,
  },
  data() {
    return {
      enteredTitle: "",
      enteredDescription: "",
      takenImageUrl: null,
      camera,
    }
  },
  methods: {
    async takePhoto() {
      const photo = await Camera.getPhoto({
        resultType: CameraResultType.Uri,
        source: CameraSource.Camera,
        quality: 60,
      })

      this.takenImageUrl = photo.webPath
    },
    submitForm() {
      const memoryData = {
        title: this.enteredTitle,
        imageUrl: this.takenImageUrl,
        description: this.enteredDescription,
      }
      this.$emit("save-memory", memoryData)
    },
  },
}
</script>

<style scoped>
div {
  margin: 0 1rem 0 1rem;
  justify-content: center;
  align-items: center;
  align-content: center;
  text-align: center;
}

ion-button {
  margin: 1rem 0rem 1rem 0;
}

ion-item {
  margin: 0rem 0rem 1rem 0;
}

img {
  margin: 1rem 0rem 1rem 0;
  border-radius: 4px;
}
</style>