<template>
  <div id="app">
    .
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <p class="lead">
          Treinando transição/animação de elementos/components no Vue.
        </p>
      </div>
    </div>
    <div class="container">
      <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">
        Alternar
      </button>
      <transition
        appear
        appear-class=""
        appear-active-class="animated flipInY"
        appear-to-class=""
        @before-appear="beforeAppear"
        @appear="appear"
        @after-appear="afterAppear"
        @appear-cancelled="appearCancelled"
        enter-active-class="animated bounceInLeft"
        leave-active-class="animated bounceOutDown"
      >
        <div class="alert alert-primary" v-if="mostrar">Animações no Vue</div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      mostrar: true,
    };
  },
  methods: {
    beforeAppear(el) {
      console.log("beforeAppear");
      el;
    },
    appear(el, done) {
      console.log("appear");
      el;
      setTimeout(done, 1000);
    },
    afterAppear(el) {
      console.log("afterAppear");
      el;
    },
    appearCancelled(el) {
      el;
      console.log("appearCancelled");
    },
    beforeEnter(el) {
      el.style.opacity = 0;
      el.style.transition = "opacity 0.1s";
      console.log("beforeEnter");
    },
    enter(el, done) {
      console.log("enter");
      let count = 0;
      const interval = setInterval(() => {
        el.style.opacity = count * 0.1;
        count++;
        if (count > 10) {
          clearInterval(interval);
          done();
        }
      }, 100);
    },
    afterEnter(el) {
      el;
      console.log("afterEnter");
    },
    enterCancelled(el) {
      el;
      console.log("enterCancelled");
    },
    beforeLeave(el) {
      el.style.transition = "width 0.1s ease-in-out";
      el.style.overflow = "hidden";
      el.style.whiteSpace = "nowrap";
    },
    leave(el, done) {
      console.log("leave");
      let count = 0;
      const width = el.offsetWidth;
      const interval = setInterval(() => {
        el.style.width = width * (1 - count / 10) + "px";
        count++;
        console.log(el.style.width);
        if (count > 10) {
          clearInterval(interval);
          done();
        }
      }, 100);
    },
    afterLeave(el) {
      el;
      console.log("afterLeave");
    },
    leaveCancelled(el) {
      el;
      console.log("leaveCancelled");
    },
  },
};
</script>
<style>
body {
  overflow: hidden;
}
</style>
<style scoped>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}

.fade-enter-to,
.fade-leave {
  opacity: 1;
}

.zoom-enter,
.zoom-leave-to {
  transform: scale(0);
}

.zoom-enter-active,
.zoom-leave-active {
  transition: transform 0.5s;
}

.zoom-enter-to,
.zoom-leave {
  transform: scale(1);
}

.slide-enter {
  opacity: 0;
}

.slide-enter-active {
  animation: slide 0.5s ease-in-out forwards;
  transition: opacity 0.5s;
}

.slide-leave-active {
  animation: slide 0.5s ease-in-out reverse;
  transition: opacity 2s; /* Essa diferença de tempo da transition com a animation causa conflito, por isso
  a propriedade type='animation' foi inserida no elemento html*/
}

.slide-leave-to {
  opacity: 0;
}

@keyframes slide {
  0% {
    transform: translateX(-100px);
  }
  100% {
    transform: translateX(0px);
  }
}
</style>
