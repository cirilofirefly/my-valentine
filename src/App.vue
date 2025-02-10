<template>
  <main>
    <h1>{{ sheSaidYes ? 'I know you will say YES, See you on Febuary 14! I love you so muuuch!' : 'Will you be my valentine?' }}</h1>
    <img 
      width="300" 
      height="300" v-if="(currentImageIndex <= images.length - 1) || currentImageIndex !== -1" :src="currentImage" alt="Not found :(">
    <div class="btns-container" v-if="!sheSaidYes">
      {{ yesBtnStyle }}
      <button ref="yesBtn" type="button" :style="[`width:${yesBtnSize}px`, `height:${yesBtnSize === 100 ? '100%' : yesBtnSize}px`]" class="btn yes-btn" @click="changeToYesImage">
        Yes {{ currentImageIndex === -1 ? "PLEAAAAAAAAAAAAASE! :'( " : '' }}
      </button>
      <button v-if="currentImageIndex >= 0" type="button" class="btn no-btn" @click="changeImage">
        No
      </button>
    </div>
    <h1 v-else style="font-size: 18px; margin-top: 20px;">You can't say NO anymore!</h1>
  </main>
</template>
<script setup>
import { computed, ref } from 'vue';

const currentImageIndex = ref(0);
const yesBtn = ref(null);
const noCount = ref(0);
const sheSaidYes = ref(false);

const yesBtnSize = ref(100);

const messages = [
  'Will you be my valentine?',
  ''
];

const images = [
  'anim1.gif',
  'anim2.gif',
  'anim3.gif',
  'anim4.gif',
  'yes.gif'
];

const changeImage = () => {
  if(currentImageIndex.value <= (images.length - 3)) {
    yesBtnSize.value = yesBtnSize.value * 1.5;
    currentImageIndex.value += 1
  } else {
    currentImageIndex.value = -1
    yesBtnSize.value = yesBtnSize.value * 1.5;
  }
}

const changeToYesImage = () => {
  sheSaidYes.value = true;
  currentImageIndex.value = images.length - 1;
}

const currentImage = computed(() => images[currentImageIndex.value]);
</script>