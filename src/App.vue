<template>
  <div class="container">
    <form novalidate>
      <transition name="slide-fade">
        <div v-show="step === 1" class="step">
          <Name v-on:nextStep="nextStep" />
        </div>
      </transition>

      <transition name="slide-fade">
        <div v-show="step === 2" class="step">
          <Client v-on:backStep="backStep" v-on:nextStep="nextStep" />
        </div>
      </transition>

      <transition name="slide-fade">
        <div v-show="step === 3" class="step">
          <Direction v-on:backStep="backStep" v-on:nextStep="nextStep" />
        </div>
      </transition>

      <transition name="slide-fade">
        <div v-show="step === 4" class="step">
          <Passport v-on:backStep="backStep" v-on:nextStep="nextStep" />
        </div>
      </transition>
    </form>
  </div>
</template>

<script>
import Name from "./components/Name";
import Client from "./components/Client";
import Direction from "./components/Direction";
import Passport from "./components/Passport.vue";
export default {
  name: "app",
  components: {
    Name,
    Client,
    Direction,
    Passport,
  },
  data() {
    return {
      step: 1,
    };
  },
  methods: {
    nextStep() {
      this.step++;
    },
    backStep() {
      this.step--;
    },
  },
};
</script>

<style lang="scss">
.slide-fade-enter-active {
  transition: all 0.5s ease;
}
.slide-fade-enter {
  transform: translateX(10px);
  opacity: 0;
}
</style>
