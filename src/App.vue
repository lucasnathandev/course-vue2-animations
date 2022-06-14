<template>
  <div id="app">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <p class="lead">
          Treinando transição/animação de elementos/components no Vue.
        </p>
      </div>
    </div>
    <div class="container">
      <h3 class="font-weight-light">State animations / Transitioning State</h3>
      <div class="form-group">
        <label for="input-number"></label>
        <input
          v-model="number"
          type="number"
          name=""
          step="50"
          id="input-number"
          class="form-control"
          placeholder=""
          aria-describedby="helpId"
        />
      </div>
      <div class="alert alert-info">
        <h3 class="font-weight-light">
          <strong>Number: </strong><span>{{ animatedNumber }}</span>
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";
export default {
  name: "App",
  data() {
    return {
      number: 0,
      interpolatedNumber: 0,
    };
  },
  computed: {
    animatedNumber() {
      return this.interpolatedNumber.toFixed(0);
    },
  },
  watch: {
    number(current) {
      gsap.to(this.$data, 2, {
        interpolatedNumber: current,
      });
    },
  },
};
</script>