<script >
import { animate, stagger} from "motion";

export default {
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  unmounted() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll(event) {
      const animationBox = animate(
        ".box",
        { y: -400 },
        {
          duration: 0.3,
          easing: [0.22, 0.03, 0.26, 1],
        }
      );
    },
  },
};
</script>

<template>
  <div>
    <div class="wrapper">
      <div class="typing-demo">&lt; hi im Gian Luca /&gt;</div>
    </div>
    <br>
    <br>
    <div style="display:flex; justify-content: center;">
      <div class="box box1"> About Me</div>
      <div class="box"></div>
    </div>
    
  </div>
</template>



<style>
@import url("https://fonts.googleapis.com/css2?family=Margarine&family=Space+Mono:ital,wght@0,400;&display=swap");
* {
  background-color: rgb(32, 32, 32);
  cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" fill="rgb(212, 204, 204)" stroke="%23000000" width="20px" height="20px" viewBox="0 0 10.04 10.04"><circle cx="5.02" cy="5.02" r="4.52"/></svg>')
      10 10,
    auto;
  font-family: "Space Mono", monospace;
  color: rgb(156, 155, 155);
}
/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: rgb(212, 204, 204);
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgb(68, 68, 68);
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.box {
  margin: 20px;
  width: 200px;
  height: 200px;
  background-color: rgb(156, 155, 155);
  border-radius: 15px;
}
.wrapper {
  height: 100vh;
  /*This part is important for centering*/
  display: grid;
  place-items: center;
}

.typing-demo {
  animation: typing 0.8s steps(20), blink 0.5s step-end infinite alternate;
  white-space: nowrap;
  overflow: hidden;
  border-right: 3px solid;
  font-family: "Space Mono", monospace;
  font-size: 2em;
  color: rgb(156, 155, 155);
}

@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 30%; /* Lässt die Breite sich automatisch anpassen */
  }
}

@keyframes blink {
  50% {
    border-color: transparent;
  }
}
.box1{
  width: 650px;
  color: white;
  font-family: "Space Mono", monospace;
  font-size: 2rem;
  display: flex;
  justify-content: center;

}
</style>