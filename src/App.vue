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
      <h3 class="font-weight-light">Technologies</h3>

      <div class="row">
        <div class="col-sm-2">
          <button class="btn btn-info" @click="shuffle">Embaralhar</button>
        </div>
        <div class="col-sm-10">
          <div class="form-group">
            <label for=""></label>
            <input
              @keyup.enter.exact="add"
              ref="input"
              type="text"
              name=""
              id=""
              class="form-control"
              placeholder="Inser a new item and press ENTER"
              aria-describedby="helpId"
            />
            <small id="helpId" class="text-muted">Help text</small>
          </div>
        </div>
      </div>

      <transition-group tag="ul" class="list-group" :name="'list'">
        <li
          class="list-group-item"
          v-for="(technology, index) in technologies"
          :key="technology"
        >
          <span>{{ technology }}</span>
          <button
            class="btn btn-danger btn-sm float-right"
            @click="remove(index)"
          >
            X
          </button>
        </li></transition-group
      >
    </div>
  </div>
</template>

<script>
import lodash from "lodash";
export default {
  name: "App",
  data() {
    return {
      technologies: ["JavaScript", "VueJS", "VueX", "VueRouter"],
    };
  },
  methods: {
    add(event) {
      const newItem = event.target.value;
      if (newItem) {
        const index = Math.floor(Math.random() * this.technologies.length);
        this.technologies.splice(index, 0, newItem);
        this.$refs.input.value = "";
      }
    },
    remove(index) {
      this.technologies.splice(index, 1);
    },
    shuffle() {
      this.technologies = lodash.shuffle(this.technologies);
    },
  },
};
</script>
<style scoped>
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateX(-70px);
}

.list-enter-active,
.list-leave-active,
/* New feature */ .list-move {
  transition: all 1s ease-in-out;
}

.list-leave-active {
  position: absolute;
  width: calc(100% - 100px);
}
</style>