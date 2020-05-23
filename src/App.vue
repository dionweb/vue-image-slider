<template>
  <div id="app">
    <transition-group name="fade" tag="div">
      <div v-for="i in [currentIndex]" :key="i">
        <img v-bind:src="currentImg" />
      </div>
    </transition-group>
    <a class="prev" v-on:click="prev" href="#">&#10094;</a>
    <a class="next" v-on:click="next" href="#">&#10095;</a>
    <div class="dots">
      <span
        v-for="index in images.length"
        :key="index"
        v-on:click="currentSlide(index-1)"
        class="dot"
      ></span>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      images: [
        require("./assets/1.jpg"),
        require("./assets/2.jpg"),
        require("./assets/3.jpg"),
        require("./assets/4.jpg")
      ],
      timer: null,
      currentIndex: 0
    };
  },
  mounted: function() {
    this.startSlide();
  },

  methods: {
    startSlide: function() {
      this.timer = setInterval(this.next, 6000);
    },

    next: function() {
      this.currentIndex++;
    },
    prev: function() {
      this.currentIndex--;
    },
    currentSlide: function(n) {
      this.currentIndex = n;
    }
  },

  computed: {
    currentImg: function() {
      return this.images[Math.abs(this.currentIndex) % this.images.length];
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  margin: 0px;
  overflow: hidden;
}

fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
  overflow: hidden;
  visibility: visible;
  position: absolute;
  width: 100%;
  opacity: 1;
}

.fade-enter,
.fade-leave-to {
  visibility: hidden;
  width: 100%;
  opacity: 0;
}

img {
  height: 100vh;
  width: 100%;
}

.prev,
.next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  transform: translate(0%, -50%);
  width: auto;
  padding: 16px;
  color: #fff;
  font-weight: bold;
  font-size: 18px;
  transition: 0.5s ease;
  border-radius: 0 4px 4px 0;
  text-decoration: none;
  user-select: none;
}
.next {
  right: 0;
}

.prev {
  left: 0;
}

.dots {
  position: absolute;
  bottom: 3%;
  left: 50%;
  transform: translate(-50%, 0%);
}

.dot {
  cursor: pointer;
  width: 50px;
  height: 3px;
  margin: 2px 6px;
  background-color: #fff;
  display: inline-block;
  transition: background-color 0.6s ease;
}
</style>
