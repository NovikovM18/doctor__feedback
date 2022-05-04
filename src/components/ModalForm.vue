<template>
  <div
    class="modal__container"
    tabindex="-1"
    @click.self="close"
    @keydown.esc="close"
  >
    <div class="modal">
      <span class="modal__close" @click="close">X</span>
      <div class="modal__content">
        <p class="modal__content__title">Залишити оцінку та відгук</p>

        <form class="modal__content__form"  @submit.prevent="sendFormData">
          <div class="modal__content__form__item">
            <div style="display:flex">
              <p>Представтесь:</p><p style="color:red">*</p>
            </div>
            <input v-if="!feedBack.anonim" required=!feedBack.anonim v-model="feedBack.name" class="form-input__text" id="name" type="text" placeholder="Вкажіть ваше прізвище та ім’я">
            <div style="display:flex">
              <input id="check-box" v-model="feedBack.anonim" type="checkbox">
              <label for="check-box">Анонімно</label>
            </div>
          </div>

          <div class="modal__content__form__item">
            <div style="display:flex">
              <p>Оцініть роботу лікаря:</p><p style="color:red">*</p>
            </div>
            <div class="raitingBox">
              <div class="stars">
                <div class="raiting">
                  <input required v-model="feedBack.raiting" id="raiting__star__5" type="radio" class="raiting__item" name="raiting" value="5">
                  <label for="raiting__star__5" class="raiting__label"></label>
                  <input v-model="feedBack.raiting" id="raiting__star__4" type="radio" class="raiting__item" name="raiting" value="4">
                  <label for="raiting__star__4" class="raiting__label"></label>
                  <input v-model="feedBack.raiting" id="raiting__star__3" type="radio" class="raiting__item" name="raiting" value="3">
                  <label for="raiting__star__3" class="raiting__label"></label>
                  <input v-model="feedBack.raiting" id="raiting__star__2" type="radio" class="raiting__item" name="raiting" value="2">
                  <label for="raiting__star__2" class="raiting__label"></label>
                  <input v-model="feedBack.raiting" id="raiting__star__1" type="radio" class="raiting__item" name="raiting" value="1">
                  <label for="raiting__star__1" class="raiting__label"></label>
                </div>
              </div>
              <div class="stars__description">
                <p>Дуже погано</p>
                <p>Погано</p>
                <p>Нормально</p>
                <p>Добре</p>
                <p>Дуже Добре</p>
              </div>
            </div>
          </div>
          
          <div class="modal__content__form__item">
            <p>Напишіть відгук:</p>
            <textarea v-model="feedBack.feed" class="form-input__textarea" placeholder="Вкажіть відгук до 500 символів…"></textarea>
          </div>

          <div class="modal__content__form-buttons">
            <button class="modal__content__form-buttons__reset" type="button" @click="reset">Очистити</button>
            <button v-if="feedBack.raiting" class="modal__content__form-buttons__send" type="submit">Надіслати</button>
          </div>
        </form>
      </div>
    </div>
  </div>  
</template>
<script>

export default {
  data() {
    return {
      feedBack: {
        name: '',
        anonim: false,
        raiting: 0,
        feed: ''
      },
    }
  },
  mounted () {
    this.$el.focus()
  },

  methods: {
    close () {
      this.$emit('close')
    },
    reset() {
      this.feedBack.name = '';
      this.feedBack.anonim = false;
      this.feedBack.raiting = 0;
      this.feedBack.feed = '';
    },
    sendFormData() {
      let fData = this.feedBack;
      this.$emit('sendedData', fData);
      alert('Відгук збережено успішно');
    }
  },
}
</script>
