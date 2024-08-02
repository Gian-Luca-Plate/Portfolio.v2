<script>
import { animate, stagger } from "motion";
import Popup from './popup.vue';

export default {
  components: { Popup },
  data() {
    return {
      lastScrollTop: 0, // Speichert die letzte Scrollposition
      aboutText: 'about-text',
      isPopupVisible: false
    };
  },
  created() {
    // Event Listener für Scroll-Events hinzufügen
    window.addEventListener("scroll", this.handleScroll);
  },
  unmounted() {
    // Event Listener entfernen, wenn die Komponente unmontiert wird
    this.upScroll();
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    // Methode zur Behandlung von Scroll-Events
    handleScroll() {
      const currentScrollTop = window.scrollY;

      // Überprüfen, ob nach unten oder oben gescrollt wurde
      if (currentScrollTop > this.lastScrollTop) {
        this.downScroll(); // Nach unten scrollen
      } else {
        this.upScroll(); // Nach oben scrollen
      }

      // Update der letzten Scrollposition
      this.lastScrollTop = currentScrollTop <= 0 ? 0 : currentScrollTop; // Für iOS Safari
    },
    // Methode zum Animieren bei nach unten Scrollen
    downScroll() {
      animate(
        ".animationBox",
        { x: 545, y: -250 }, // Zielposition für die Animation
        { delay: stagger(0.1), duration: 0.5, easing: [0.22, 0.03, 0.26, 1] } // Animationsoptionen
      );
    },
    // Methode zum Animieren bei nach oben Scrollen
    upScroll() {
      animate(
        ".animationBox",
        { x: -1450, y: -250 }, // Zielposition für die Animation
        { delay: stagger(0.1), duration: 0.5, easing: [0.22, 0.03, 0.26, 1] } // Animationsoptionen
      );
    },
    box1Click(){
      if( this.aboutText === 'about-text'){
        this.aboutText = 'about-textBig'
        this.togglePopup()
      }
    },
    togglePopup() {
      this.isPopupVisible = !this.isPopupVisible;
    },
  },
};
</script>


<template>
  <div>
    <button @click="togglePopup">Open Popup</button>
    <Popup v-if="isPopupVisible" @close="togglePopup">
      <h1 class="about-heading">About Me</h1>
            <p :class="aboutText">
              Hello, my name is Gian Luca. I am a passionate young developer who
              feels at home in the world of programming. My journey began at the
              age of 12 when I started learning HTML, CSS, and JavaScript. Since
              then, I have been on a continuous path of learning and growing in
              software development. Recently, I completed an exciting 2-week
              internship in Onsite IT Support in Munich. This experience not
              only enhanced my practical skills but also provided me with deep
              insights into the professional world of IT. Since the early days,
              I have not only expanded my knowledge in the fundamentals but have
              also recently been actively working with Python and Vue.js. This
              modern JavaScript library has sparked my interest and opened up
              new perspectives in web development. My goal is to continue
              learning, growing, and tackling the challenges of software
              development. The joy of coding drives me, and I am ready to apply
              my skills to new projects and challenges. Off to new horizons in
              the world of code!
            </p>
    </Popup>
    <div class="wrapper">
      <div class="typing-demo">&lt; Hi, I'm Gian Luca /&gt;</div>
    </div>
    <table>
      <tr class="animationBox">
        <td>
          <div class="box1" @click="box1Click()">
            <h1 class="about-heading">About Me</h1>
            <p :class="aboutText">
              Hello, my name is Gian Luca. I am a passiona...
            </p>
          </div>
        </td>
        <td>
          <div class="box2">
            <h1 class="work-heading">My Work</h1>
          </div>
        </td>
      </tr>
    </table>
  </div>
</template>


<style>
@import url("https://fonts.googleapis.com/css2?family=Pixelify+Sans&display=swap");

/* Globale Stile */
* {
  background-color: rgb(
    32,
    32,
    32
  ); /* Dunkler Hintergrund für die gesamte Seite */
  cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" fill="none" stroke="rgb(212, 204, 204)" width="20px" height="20px" viewBox="0 0 10.04 10.04"><circle cx="5.02" cy="5.02" r="4.52"/></svg>')
      10 10,
    auto; /* Benutzerdefinierter Cursor */
  font-family: "Pixelify Sans", sans-serif; /* Schriftart für die gesamte Seite */
}

/* Stil für die Wrapper-Div */
.wrapper {
  height: 100vh; /* Höhe des Wrappers auf 100% der Viewport-Höhe setzen */
  display: grid; /* Grid-Layout verwenden */
  place-items: center; /* Inhalt sowohl horizontal als auch vertikal zentrieren */
}

/* Typing-Animation für den Begrüßungstext */
.typing-demo {
  animation: typing 1s steps(22), blink 0.5s step-end infinite alternate; /* Animationen für das Tippen und Blinken */
  white-space: nowrap; /* Verhindert Zeilenumbrüche im Text */
  overflow: hidden; /* Verhindert, dass der Text außerhalb des Containers angezeigt wird */
  border-right: 3px solid; /* Schreibmaschinen-Cursor-Effekt durch eine rechte Rahmenlinie */
  font-family: "Pixelify Sans", sans-serif; /* Schriftart für den Text */
  font-size: 3em; /* Schriftgröße des Textes */
  color: rgb(156, 155, 155); /* Farbe des Textes */
}

/* Keyframes für die Tipp-Animation */
@keyframes typing {
  from {
    width: 0; /* Startbreite des Textes bei 0 */
  }
  to {
    width: 25%; /* Endbreite des Textes bei 25% des Containers */
  }
}

/* Keyframes für die Cursor-Blink-Animation */
@keyframes blink {
  50% {
    border-color: transparent; /* Cursor wird zur Hälfte der Zeit unsichtbar */
  }
}

/* Stil für Boxen */
.box1,
.box2 {
  padding: 20px; /* Innenabstand in den Boxen */
  background-color: #363636; /* Hintergrundfarbe der Boxen */
  transition: background-color 1s ease, color 1s ease; /* Sanfte Übergänge für Hintergrund- und Textfarbe */
  border-radius: 15px; /* Abgerundete Ecken */
  color: rgb(156, 155, 155); /* Textfarbe */
  height: 124.44px; 
}

/* Hover-Effekt für Box1 */
.box1:hover {
  background-color: #d4cccc; /* Hintergrundfarbe bei Hover */
  color: #363636; /* Textfarbe bei Hover */
}

/* Hover-Effekt für Box2 */
.box2:hover {
  background-color: #d4cccc; /* Hintergrundfarbe bei Hover */
  color: #363636; /* Textfarbe bei Hover */
}

/* Stil für Überschrift in Box1 und Box2 */
.about-heading,
.work-heading {
  font-size: 2.5rem; /* Schriftgröße für Überschriften */
  color: inherit; /* Farbe der Überschrift entsprechend der Elterneigenschaft */
  background-color: transparent; /* Hintergrundfarbe der Überschrift transparent */
  display: flex; /* Flexbox-Layout für zentrierte Ausrichtung */
  justify-content: center; /* Horizontale Zentrierung */
}

/* Stil für About-Heading mit zusätzlichem Abstand */
.about-heading {
  margin-bottom: 10px; /* Abstand unterhalb der Überschrift */
}

/* Stil für Work-Heading mit zusätzlichem Abstand oben */
.work-heading {
  margin-top: 35px; /* Abstand oberhalb der Überschrift */
}


/* Stil für den Text innerhalb von Box1 */
.about-text {
  color: inherit; /* Textfarbe entsprechend der Elterneigenschaft */
  font-size: 1rem; /* Schriftgröße des Textes */
  background-color: transparent; /* Hintergrundfarbe des Textes transparent */
  display: flex; /* Flexbox-Layout für zentrierte Ausrichtung */
  justify-content: center; /* Horizontale Zentrierung */
  overflow: clip; /* Verhindert das Überlaufen des Textes */
  width: 480.55px; /* Feste Breite des Textfeldes */
  height: 14.44px; /* Feste Höhe des Textfeldes */
}

/* Stil für Box2 */

.about-textBig {
  color: inherit; /* Textfarbe entsprechend der Elterneigenschaft */
  font-size: 1rem; /* Schriftgröße des Textes */
  background-color: transparent; /* Hintergrundfarbe des Textes transparent */
  display: flex; /* Flexbox-Layout für zentrierte Ausrichtung */
  justify-content: center; /* Horizontale Zentrierung */
  overflow: clip; /* Verhindert das Überlaufen des Textes */
  width: 490px; /* Feste Breite des Textfeldes */
  height: 390px; /* Feste Höhe des Textfeldes */
  font-size: 20px;
}
</style>
