<template>
  <div class="p-3 rounded" style="max-width: 400px; margin: 50px auto; background: #ffdce3">
    <!--calc result-->
    <div class="w-full rounded m-1 p-3 text-end lead fw-bold text-white bg-dark-pink">
      {{ calcValue || 0 }}
    </div>

    <!--calc buttons-->
    <div class="row g-0">
      <div class="col-3" v-for="n in calcElements" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 rounded bg-dark-pink hover-class"
          :class="{ 'bg-brown': ['C', '*', '/', '-', '+', '%', '='].includes(n) }"
          @click="handleClick(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import clickSoundFile from '@/assets/sounds/click-se.mp3'

export default {
  name: 'Calculator',
  data() {
    return {
      calcValue: '',
      calcElements: [
        'C',
        '*',
        '/',
        '-',
        '7',
        '8',
        '9',
        '+',
        '4',
        '5',
        '6',
        '%',
        '1',
        '2',
        '3',
        '=',
        '0',
        '.',
      ],
      operator: null,
      previousCalcValue: '',
      clickSound: new Audio(clickSoundFile),
    }
  },
  methods: {
    handleClick(n) {
      this.clickSound.play()

      /* value */
      if (!isNaN(n) || n === '.') {
        this.calcValue += n + ''
      }

      /* clear */
      if (n === 'C') {
        this.calcValue = ''
      }

      /* percentage */
      if (n === '%') {
        this.calcValue = this.calcValue / 100 + ''
      }

      /* operator */
      if (['*', '/', '-', '+'].includes(n)) {
        this.operator = n
        this.previousCalcValue = this.calcValue
        this.calcValue = ''
      }

      /* equal */
      if (n === '=') {
        this.calcValue = eval(this.previousCalcValue + this.operator + this.calcValue)
        this.previousCalcValue = ''
        this.operator = null
      }
    },
  },
}
</script>

<style scoped>
.bg-dark-pink {
  background: #f4acb7;
}
.hover-class:hover {
  cursor: pointer;
  background: #ffbec8;
}
.bg-brown {
  background: #ac9299;
}
</style>
