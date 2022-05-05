<template>
  <div class="home">
    <loading
      v-model:active="isLoading"
      :is-full-page="true"
      color="#3fa9f5"
      background-color="black"
      :opacity="0.9"
      blur="100px"
      transition="loader" />

    <TransitionGroup name="inputs">
      <img src="@/assets/logo.png" alt="Logo" class="logo" key="1">
      <div key="announce" class="announce" v-if="correct">
        <span class="date">
          10th May
        </span>
        <span class="label">
          to infinity and beyond
        </span>
      </div>
      <TransitionGroup name="inputs" key="inputs" tag="div" class="input-master" v-else>
        <form @submit.prevent="handleInput" class="input-wrapper" key="2">
          <input type="text" class="password" v-model="input">
          <button type="submit" class="enter">Enter</button>
        </form>
        <span key="3" v-if="hint" class="hint">
          <span class="pass">#to_infinity</span>
          <span class="label" dir="rtl">كلمة السر: </span>
        </span>
      </TransitionGroup>
    </TransitionGroup>
  </div>
</template>

<script>
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';

export default {
  name: 'HomeView',
  data() {
    return {
      input: '',
      correct: null,
      hint: null,
      isLoading: false
    }
  },
  components: {
    Loading
  },
  methods: {
    handleInput() {
      if (!this.input) return
      if (this.input == '#to_infinity') {
        this.isLoading = true
        setTimeout(() => {
          this.isLoading = false;
          this.correct = true
        }, Math.floor(Math.random() * 4000))
      } else {
        this.hint = true
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.inputs-move, /* apply transition to moving elements */
.inputs-enter-active,
.inputs-leave-active {
  transition: all 0.4s ease;
}

.inputs-enter-from,
.inputs-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.inputs-leave-active {
  position: absolute;
}

.announce {
  color: $blue;
  font-size: 2rem;
  display: flex;
  font-weight: 800;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  line-height: 65px;
  text-align: center;

  .date {
    font-weight: 200;
    font-size: 1.8rem;
    opacity: 0.7;
  }
}

.home {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  z-index: 100;
  padding: 20px;

  .hint {
    color: lighten($blue, 10%);
    font-size: 0.7rem;
    margin-top: 20px;
    text-align: center;

    .label {
      font-weight: 600;
      margin-left: 5px;
      user-select: none;
    }
  }

  .logo {
    position: fixed;
    top: 100px;
    height: 250px;
    left: 50%;
    transform: translateX(-50%);
  }

  .input-master {
    display: flex;
    justify-content: center;
    align-content: center;
    flex-direction: column;
    width: 900px;
    max-width: 100%;
  }

  .input-wrapper {
    width: 100%;
    height: 70px;
    display: flex;

    .password {
      flex: 1;
      height: 100%;
      background: transparent;
      border-radius: 10px;
      border: none;
      outline: none;
      margin-right: 10px;
      font-size: 0.8rem;
      text-align: center;
      color: $blue;
      font-family: inherit;
      // animation: glow 800ms ease-out infinite alternate;
      box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.5),
        0px 0px 26px 0px rgba(63, 169, 245, 0.3), 0px 0px 0px 1px $blue;

      -webkit-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.5),
        0px 0px 26px 0px rgba(63, 169, 245, 0.3), 0px 0px 0px 1px $blue;

      -moz-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.5),
        0px 0px 26px 0px rgba(63, 169, 245, 0.3), 0px 0px 0px 1px $blue;
      transition: box-shadow 0.2s linear;

      &:focus {
        box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.7),
          0px 0px 26px 0px rgba(63, 169, 245, 0.5), 0px 0px 0px 3px $blue;

        -webkit-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.7),
          0px 0px 26px 0px rgba(63, 169, 245, 0.5), 0px 0px 0px 3px $blue;

        -moz-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.7),
          0px 0px 26px 0px rgba(63, 169, 245, 0.5), 0px 0px 0px 3px $blue;
      }
    }

    @keyframes glow {
      0% {
        border-color: #393;
        box-shadow: 0 0 5px opacify($blue, 0.2),
          inset 0 0 5px opacify($blue, 0.1), 0 2px 0 #000;
      }
      100% {
        border-color: #6f6;
        box-shadow: 0 0 20px opacify($blue, 0.6),
          inset 0 0 10px opacify($blue, 0.4), 0 2px 0 #000;
      }
    }

    .enter {
      color: $dark_blue;
      font-family: inherit;
      height: 100%;
      border-radius: 10px;
      background: $blue;
      border: none;
      font-size: 0.8rem;
      display: flex;
      justify-content: center;
      align-items: center;
      font-weight: 700;
      cursor: pointer;
      user-select: none;
      padding: 0 30px;
      white-space: nowrap;
      overflow: hidden;
      box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.7),
        0px 0px 26px 0px rgba(63, 169, 245, 0.5);
      -webkit-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.7),
        0px 0px 26px 0px rgba(63, 169, 245, 0.5);
      -moz-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.7),
        0px 0px 26px 0px rgba(63, 169, 245, 0.5);
      transition: box-shadow 0.2s linear, transform 0.2s ease;

      &::before {
        content: "←";
        margin-right: 10px;
      }

      &:hover {
        transform: translateY(-2px);
        box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.9),
          0px 0px 26px 0px rgba(63, 169, 245, 0.7);
        -webkit-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.9),
          0px 0px 26px 0px rgba(63, 169, 245, 0.7);
        -moz-box-shadow: inset 0px 0px 20px 0px rgba(63, 169, 245, 0.9),
          0px 0px 26px 0px rgba(63, 169, 245, 0.7);
      }

      &:active {
        transform: translateY(1px);
      }
    }
  }

  .loader-enter-active,
  .loader-leave-active {
    transition: all 0.5s ease;
  }
  .loader-enter-from,
  .loader-leave-to {
    opacity: 0;
  }

  @media screen and (max-width: 600px) {
    .logo {
      position: fixed;
      top: 30px;
      height: 150px;
      left: 50%;
      transform: translateX(-50%);
    }

    .enter {
      &::before {
        content: "↑" !important;
      }
    }
    .password {
      border: 1px solid $blue !important;
    }
    .input-wrapper {
      flex-direction: column;
      height: 120px;

      .password {
        flex: initial;
        margin-right: 0;
        margin-bottom: 10px;
      }
    }

    .announce {
      font-size: 1rem;
      line-height: 32px;

      .date {
        font-size: inherit;
      }
    }
  }
}
</style>
