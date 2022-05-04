<template>
  <div class="header">
    <div class="header__container container">
      <p class="header__title">Проіфль лікаря</p>
    </div>
  </div>
  <div class="container">
    <div class="info">
      <div class="info__title">
        <p class="info__title-name">Ремі Борегард Хедлі</p>
        <div class="info__title-raiting">
          <div class="info__title-raiting__stars">
            <div v-if="stars >= 1" class="info__title-raiting__stars__item">★</div>
            <div v-if="stars >= 2" class="info__title-raiting__stars__item">★</div>
            <div v-if="stars >= 3" class="info__title-raiting__stars__item">★</div>
            <div v-if="stars >= 4" class="info__title-raiting__stars__item">★</div>
            <div v-if="stars >= 5" class="info__title-raiting__stars__item">★</div>
          </div>
          <p>(Середня оцінка: {{stars}})</p>
        </div>
      </div>

      <div class="info__details">
        <div class="info__details-photo"></div>
        <div class="info__details-text">
          <div class="info__details-text__item">
            <p class="info__details-text__item-title">Місто:</p>
            <p class="info__details-text__item-description">Львів</p>
          </div>
          
          <div class="info__details-text__item">
            <p class="info__details-text__item-title">Місце роботи:</p>
            <p class="info__details-text__item-description">Львів, Площа Ринок, 14</p>
          </div>

          <div class="info__details-text__item">
            <p class="info__details-text__item-title">Заклад:</p>
            <p class="info__details-text__item-description"><a href="https://www.facebook.com/kryjivkalviv/">Відділення екстренної допомоги</a></p>
          </div>
          <div
            class="feeds"
            v-if="feedBacks.length > 0"
          >
            <p class="feeds__title">Відгуки:</p>
            <div 
              class="feend__item" 
              v-for="f in feedBacks.slice(slicerStart, slicerEnd)" :key="f"
            >
              Ім’я:{{ f.name }},
              Оцінка:{{ f.raiting }}
              Відгук:{{ f.feed }}
            </div>
            <button class="slice-button" v-if="feedBacks.length > 5" @click="prevSlice">назад</button>
            <button class="slice-button__next" v-if="feedBacks.length > 5" @click="nextSlice">наступні</button>
          </div>
          <button
            class="info__details-button"
            @click="modalOpen = true"
          >
            Залишити оцінку та відгук
          </button>
        </div>
      </div>
    </div>
  </div>

  <ModalForm
    v-if="modalOpen"
    @close="modalOpen = false"
    @sendedData="sendFeed"
  />
</template>

<script>
import ModalForm from './components/ModalForm.vue';

export default {
  components: { ModalForm },
  data() {
    return {
      modalOpen: false,
      feedBacks: [],
      stars: 0,
      starsCalc: 0,
      slicerStart: 0,
      slicerEnd: 5
    }
  },
  methods: {
    sendFeed(data) {
      this.feedBacks = [...this.feedBacks, data];
      this.starsCalc += Number(data.raiting);
      this.modalOpen = false;
      this.stars = Math.ceil(this.starsCalc / this.feedBacks.length);
    },
    nextSlice() {
      if (this.feedBacks.length > this.slicerEnd) {
        this.slicerStart += 5;
        this.slicerEnd += 5;
      }
    },
    prevSlice() {
      if (this.slicerStart > 0) {
        this.slicerStart -= 5;
        this.slicerEnd -= 5;
      }
        console.log(this.slicerStart);
    },
  }
}
</script>
