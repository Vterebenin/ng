<template lang="pug">
  div
    - var n = 0;
    while n < 200
      .snow
      - n++
    v-container(style="border-radius: 20px; background-color: rgba(20,20,20,0.75)")
      v-row
        v-col(offset="4" cols="4")
          .poem-wrapper.poem-fade
            .poem {{ qText }}
            v-text-field(
              v-model="answer"
              max-width="300"
              dark
              :color="color"
              label="Ответ"
              @click:append="handleQuestionApply(answer)"
              append-icon="mdi-check")
</template>

<script>
export default {
  name: 'ng',
  data () {
    return {
      qText: '...а внеземных среди конструкций иллюзорных,\n\n' +
        'Где слово не проронишь без надзора,\n\n' +
        'Сияние её портретов умилённых,\n\n' +
        'ласкают очи зрителя зазорно.\n\n\n\n',
      answer: '',
      color: '#fff'
    }
  },
  methods: {
    handleAnswer (n) {
      if (n === 1) {
        const nuxt = document.getElementById('__nuxt')
        nuxt.classList.add('stage-1')
        this.qText = 'Вспомнив любимую привычку, \n\n' +
          'Уставше, ты посмотришь сквозь него,\n\n' +
          'Лишь оглядевшись, ты заметишь: \n\n' +
          'Нет, не ключ, отмычку...\n\n' +
          'Что требует тепло.\n\n\n\n'
      } else if (n === 2) {
        const nuxt = document.getElementById('__nuxt')
        nuxt.classList.add('stage-2')
        this.qText = '"О боги, разверните судно!": молит, \n\n' +
          'несуществующий капитан,\n\n' +
          'Который, стало быть должен, плыть по волнам \n\n ' +
          'руля короблем на пределе,\n\n' +
          'который, на самом деле, \n\n' +
          'Призрак из пластика...\n\n\n\n'
      } else if (n === 3) {
        const snow = document.getElementsByClassName('snow')
        for (let i = 0, all = snow.length; i < all; i++) {
          snow[i].classList.add('active')
        }
        this.qText = 'Поздравляем, Полина! \n\n' +
          'Вы правильно ответили на все вопросы! \n\n' +
          'Поэтому вот ваш приз: \n\n' +
          'Зимой и летом одним цветом. \n\n'
      }
      // обработать фронт и перевести текст
    },
    handleQuestionApply (answer) {
      answer = parseFloat(answer)
      switch (answer) {
        case 17343:
          console.log(17343)
          this.handleAnswer(1)
          break
        case 88324:
          console.log(88324)
          this.handleAnswer(2)
          break
        case 73:
          alert('Ты пидор')
          break
        case 73621:
          console.log(73621)
          this.handleAnswer(3)
          break
        default:
          alert('Неправильно')
          break
      }
    }
  }
}
</script>
<style lang="scss">
  body {
    position: relative;
    overflow: hidden;
    min-height: 100vh;
  }
  #__nuxt {
    background: black;
    display: block;
    top: 0;
    left: 0;
    width: 100%;
    min-height: 100vh;
    height: 100%;
    filter: grayscale(100%);
    transition: background 0.75s,filter 0.75s;
    &.stage-1 {
      background: #db5e6c url('../assets/ponytown.png') no-repeat 0 0;
      background-size: cover;
      filter: grayscale(100%);
    }
    &.stage-2 {
      filter: grayscale(0);
    }
  }
  .poem-wrapper {
    margin: -4000px;
    padding: 4000px;
    box-sizing: content-box;
    background-color: black;
    justify-content: center;
    transition: background-color 1s;
  }
  .poem {
    color: #fff;
    white-space: pre;
  }
  .poem-fade {
    background: transparent;
  }

  /* snow */
 body {
    height: 100vh;
    background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
    overflow: hidden;
    filter: drop-shadow(0 0 10px white);
  }

  @function random_range($min, $max) {
    $rand: random();
    $random_range: $min + floor($rand * (($max - $min) + 10));
    @return $random_range;
  }

  .snow {
    $total: 200;
    position: absolute;
    width: 10px;
    height: 10px;
    background: white;
    border-radius: 50%;
    opacity: 0;
    transition: opacity 2.25s;
    &.active {
      opacity: 1;
      @for $i from 1 through $total {
        $random-x: random(1000000) * 0.0001vw;
        $random-offset: random_range(-100000, 100000) * 0.0001vw;
        $random-x-end: $random-x + $random-offset;
        $random-x-end-yoyo: $random-x + ($random-offset / 2);
        $random-yoyo-time: random_range(30000, 80000) / 100000;
        $random-yoyo-y: $random-yoyo-time * 100vh;
        $random-scale: random(10000) * 0.0001;
        $fall-duration: random_range(10, 30) * 1s;
        $fall-delay: random(30) * -1s;

        &:nth-child(#{$i}) {
          opacity: random(10000) * 0.0001;
          transform: translate($random-x, -10px) scale($random-scale);
          animation: fall-#{$i} $fall-duration $fall-delay linear infinite;
        }

        @keyframes fall-#{$i} {
          #{percentage($random-yoyo-time)} {
            transform: translate($random-x-end, $random-yoyo-y) scale($random-scale);
          }

          to {
            transform: translate($random-x-end-yoyo, 100vh) scale($random-scale);
          }
        }
      }
    }
  }

</style>
