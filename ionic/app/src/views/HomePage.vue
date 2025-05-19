<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Rádio Rede Aleluia</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding text-center">
      <!--<img src="/assets/icon192.png" alt="Logo Rádio" class="logo" />-->
      <h2>A voz da fé e da esperança</h2>

      <div class="player">
        <p>{{ trackLabel }}</p>
        <audio ref="audioPlayer" :src="streamUrl"></audio>
        <ion-button :color="isPlaying ? 'danger' : 'primary'" @click="togglePlay">
          <ion-icon :icon="isPlaying ? 'pause' : 'play'" slot="start" />
          {{ isPlaying ? 'Pausar' : 'Ouvir' }}
        </ion-button>
        <ion-range max="1" min="0" pin snaps step="0.01" value="1" @ionChange="onVolumeChange($event)">
          <ion-icon slot="start" icon="volume-high" />
        </ion-range>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonButton, IonIcon, IonRange } from '@ionic/vue';

const streamUrl = 'https://glaudiotecnology.srv.br/listen/r%C3%A1dio_rede_aleluia_100.5_fm_/100.5';
const audioPlayer = ref<HTMLAudioElement>();
const isPlaying = ref(false);
const trackLabel = ref('Transmissão ao vivo');

function togglePlay() {
  if (!isPlaying.value) {
    audioPlayer.value?.play();
  } else {
    audioPlayer.value?.pause();
  }
  isPlaying.value = !isPlaying.value;
}

function onVolumeChange(event: any) {
  audioPlayer.value!.volume = event.detail.value;
}
</script>

<style scoped>
.logo { width: 120px; border-radius: 50%; margin-bottom: 16px; }
.player { display: flex; flex-direction: column; gap: 12px; align-items: center; }
h2 { margin-bottom: 24px; font-weight: 500; }
</style>