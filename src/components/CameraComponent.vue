<template>
  <ion-card class="camera-card">
    <ion-card-content class="ion-text-center ion-padding-vertical">
      <ion-button 
        expand="block" 
        color="primary" 
        shape="round" 
        size="large" 
        @click="takePicture" 
        class="capture-btn"
      >
        <ion-icon slot="start" :icon="cameraIcon" size="large" />
        Take Picture
      </ion-button>
      
      <ion-text v-if="errorMessage" color="danger" class="ion-margin-top">
        <p class="error-text">{{ errorMessage }}</p>
      </ion-text>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import { IonCard, IonCardContent, IonButton, IonIcon, IonText } from "@ionic/vue";
import { camera as cameraIcon } from "ionicons/icons";
import { Camera } from "@capacitor/camera";
import { ref } from "vue";

const errorMessage = ref("");
const emit = defineEmits<{ (e: "photo-captured", photo: string): void }>();

const takePicture = async () => {
  errorMessage.value = "";
  try {
    const photo = await Camera.takePhoto({ quality: 90, saveToGallery: false });
    if (photo.webPath) {
      emit("photo-captured", photo.webPath);
    }
  } catch (error: any) {
    errorMessage.value = error.message || "Error taking picture.";
  }
};
</script>

<style scoped>
.camera-card {
  margin: 0;
  box-shadow: none;
  background: transparent;
}

.capture-btn {
  font-weight: 600;
  letter-spacing: 0.5px;
  box-shadow: 0 4px 12px rgba(var(--ion-color-primary-rgb), 0.3);
  margin-top: 8px;
}

.error-text {
  font-size: 0.9rem;
  font-weight: 500;
  margin-top: 12px;
}
</style>