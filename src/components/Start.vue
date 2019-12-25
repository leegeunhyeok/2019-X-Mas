<template>
  <div class="start">
    <div class="start__image" :class="toTop ? 'toTop' : ''">
      <img alt="Present box" src="@/assets/logo.png">
    </div>
    <transition name="fade" mode="out-in">
      <div class="start__input" v-if="showInput">
        <textarea v-model="myCode" spellcheck="false"></textarea>
        <button @click="sendCodeToSanta">Go!</button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'Start',
  data () {
    return {
      toTop: false,
      showInput: false,
      myCode: ''
    }
  },
  mounted () {
    setTimeout(() => {
      this.toTop = true

      setTimeout(() => {
        this.showInput = true
      }, 300)
    }, 500)
  },
  methods: {
    sendCodeToSanta () {
      if (!this.myCode) {
        alert('코드가 필요합니다!')
      }
      this.$emit('sendCode', this.myCode)
    }
  }
}
</script>
<style scoped lang="scss">
.start {
  width: 100%;
  height: 100%;
  padding: 20px;

  &__image {
    position: absolute;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%, -50%);
            transform: translate(-50%, -50%);
    -webkit-transition: .4s;
            transition: .4s;

    &.toTop {
      top: 160px;
    }
  }

  &__input {
    position: relative;
    top: 280px;
    width: 100%;
    max-width: 500px;
    height: 350px;
    margin: auto;
    margin-bottom: 30px;

    textarea {
      width: 100%;
      height: 100%;
      resize: none;
      border: 2px solid #000;
      border-radius: 4px;
    }

    button {
      cursor: pointer;
      margin-top: 10px;
      border-radius: 4px;
      width: 100%;
      border: 2px solid #fff;
      color: #fff;
      font-size: 2rem;
      background-color: red;
      box-shadow: 0 0 10px rgba(0, 0, 0, .5);
      -webkit-transition: background-color .2s;
              transition: background-color .2s;

      &:hover {
        background-color: darken(red, 10%);
      }
    }
  }
}
</style>
