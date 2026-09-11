<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title class="ion-text-center">
          <ion-icon :icon="imagesIcon" style="margin-right: 8px; vertical-align: middle;" />
          My Photo Gallery
        </ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content class="ion-padding" :fullscreen="true">
      <CameraComponent @photo-captured="addPhoto" />
      <PhotoGalleryComponent :photos="photos" />
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonIcon
} from "@ionic/vue";
import { ref } from "vue";
import { images as imagesIcon } from "ionicons/icons";
import CameraComponent from "@/components/CameraComponent.vue";
import PhotoGalleryComponent from "@/components/PhotoGalleryComponent.vue";

const photos = ref<string[]>([]);

const addPhoto = (photo: string) => {
  photos.value.unshift(photo);
};
</script>

<style scoped>
ion-toolbar {
  --background: var(--ion-color-primary);
  --color: var(--ion-color-primary-contrast);
}

ion-title {
  font-weight: 700;
  letter-spacing: 0.5px;
  font-size: 1.1rem;
}
</style>