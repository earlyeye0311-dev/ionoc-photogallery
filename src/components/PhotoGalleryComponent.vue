<template>
  <div class="gallery-container">
    <!-- Empty State -->
    <div v-if="photos.length === 0" class="empty-gallery ion-text-center ion-padding">
      <ion-icon :icon="imageOutline" size="large" color="medium" class="empty-icon" />
      <h3>No pictures yet</h3>
      <p class="ion-text-wrap">Tap the camera button above to capture your first memory!</p>
    </div>
    
    <!-- Photo Grid -->
    <ion-grid v-else class="photo-grid">
      <ion-row>
        <ion-col v-for="(photo, index) in photos" :key="index" size="6" size-md="4" size-lg="3">
          <div class="photo-wrapper">
            <ion-img :src="photo" class="gallery-image" />
          </div>
        </ion-col>
      </ion-row>
    </ion-grid>
  </div>
</template>

<script setup lang="ts">
import { IonGrid, IonRow, IonCol, IonImg, IonIcon } from "@ionic/vue";
import { imageOutline } from "ionicons/icons";

defineProps<{ photos: string[] }>();
</script>

<style scoped>
.gallery-container {
  margin-top: 8px;
}

/* Empty State Styling */
.empty-gallery {
  padding: 40px 20px;
  background: var(--ion-color-light);
  border-radius: 16px;
  border: 2px dashed var(--ion-color-medium);
}

.empty-icon {
  font-size: 48px;
  margin-bottom: 12px;
  opacity: 0.6;
}

.empty-gallery h3 {
  margin: 8px 0 4px;
  color: var(--ion-color-dark);
  font-weight: 600;
}

.empty-gallery p {
  color: var(--ion-color-medium);
  font-size: 0.9rem;
}

/* Grid & Image Styling */
.photo-grid {
  --ion-grid-padding: 8px;
}

.photo-wrapper {
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.08);
  transition: transform 0.2s ease;
  background: var(--ion-color-light);
}

.photo-wrapper:active {
  transform: scale(0.97); /* Subtle press effect on mobile */
}

.gallery-image {
  width: 100%;
  height: 160px;
  display: block;
}

.gallery-image::part(image) {
  object-fit: cover;
}
</style>