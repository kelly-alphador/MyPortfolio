<template>
  <div id="app">
    <!-- Social Media Sidebar -->
    <div class="social-sidebar">
      <div class="social-line"></div>
      <div class="social-icons">
        <a href="tel:+261345238397" class="social-icon" aria-label="Téléphone">
          <Phone class="icon" />
          <span class="tooltip">+261 34 52 383 97</span>
        </a>
        <a
          href="mailto:kelly@example.com"
          class="social-icon"
          aria-label="Email"
        >
          <Mail class="icon" />
          <span class="tooltip">kellyalphador@gmail.com</span>
        </a>
        <a
          href="https://github.com/kelly-alphador"
          target="_blank"
          class="social-icon"
          aria-label="GitHub"
        >
          <Github class="icon" />
          <span class="tooltip">GitHub</span>
        </a>
        <a
          href="https://www.linkedin.com/in/kelly-alphador-990803362/"
          target="_blank"
          class="social-icon"
          aria-label="LinkedIn"
        >
          <Linkedin class="icon" />
          <span class="tooltip">LinkedIn</span>
        </a>
      </div>
    </div>

    <!-- Main Content Container -->
    <div class="main-content">
      <div id="home" class="section-container">
        <!-- Blur Background for Home - seulement dans cette section -->
        <div class="blur-bg-home"></div>
        <Home />
      </div>
      <div id="about">
        <About />
      </div>
      <div id="skills">
        <Skills />
      </div>
      <div id="experience">
        <Experience />
      </div>
      <div id="projects">
        <Projects />
      </div>
      <div id="contact">
        <Contact />
      </div>
    </div>

    <!-- Particles Background -->
    <div class="particles" ref="particles"></div>
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Skills from "./components/Skills.vue";
import Experience from "./components/Experience.vue";
import Projects from "./components/Projects.vue";
import Contact from "./components/Contact.vue";
import About from "./components/About.vue";
import { Phone, Mail, Github, Linkedin } from "lucide-vue-next";

export default {
  name: "App",
  components: {
    Home,
    Skills,
    About,
    Experience,
    Projects,
    Contact,
    Phone,
    Mail,
    Github,
    Linkedin,
  },
  mounted() {
    this.createParticles();
  },
  methods: {
    createParticles() {
      const particlesContainer = this.$refs.particles;
      const particleCount = 50;

      for (let i = 0; i < particleCount; i++) {
        const particle = document.createElement("div");
        particle.className = "particle";
        particle.style.left = Math.random() * 100 + "%";
        particle.style.top = Math.random() * 100 + "%";
        particle.style.animationDelay = Math.random() * 3 + "s";
        particlesContainer.appendChild(particle);
      }
    },
  },
};
</script>

<style>
/* Import Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Jost:ital,wght@0,100..900;1,100..900&display=swap');
/* Variables de couleurs */
:root {
  --emerald-primary: #50c878;
  --emerald-dark: #2e8b57;
  --text-primary: #ffffff;
  --text-secondary: #e8f5e9;
  --bg-dark: #161916;
}

/* Global Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  width: 100%;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Jost", sans-serif;
  font-weight: 500;
  background: var(--bg-dark);
  min-height: 100vh;
  overflow-x: hidden;
  color: var(--text-primary);
  background-attachment: fixed;
  width: 100%;
  margin: 0;
  padding: 0;
}

/* App Container */
#app {
  position: relative;
  width: 100%;
  min-height: 100vh;
  padding: 20px;
}

/* Social Media Sidebar */
.social-sidebar {
  position: fixed;
  left: 30px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 30px;
  z-index: 100;
}

.social-line {
  width: 1px;
  height: 100px;
  background: linear-gradient(
    to bottom,
    transparent,
    var(--emerald-primary),
    transparent
  );
}

.social-icons {
  display: flex;
  flex-direction: column;
  gap: 25px;
  align-items: center;
}

.social-icon {
  position: relative;
  width: 45px;
  height: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: rgba(22, 25, 22, 0.7);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: var(--text-secondary);
  text-decoration: none;
  transition: all 0.3s ease;
  cursor: pointer;
  backdrop-filter: blur(5px);
}

.social-icon:hover {
  transform: translateY(-5px);
  background: var(--emerald-primary);
  color: var(--bg-dark);
  border-color: var(--emerald-primary);
  box-shadow: 0 5px 15px rgba(80, 200, 120, 0.3);
}

.social-icon:hover .icon {
  color: var(--bg-dark);
}

.social-icon .icon {
  width: 22px;
  height: 22px;
  transition: all 0.3s ease;
}

/* Tooltip */
.tooltip {
  position: absolute;
  left: 60px;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(22, 25, 22, 0.9);
  color: var(--text-primary);
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 0.9rem;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  border: 1px solid rgba(80, 200, 120, 0.2);
  pointer-events: none;
  z-index: 101;
}

.tooltip::before {
  content: "";
  position: absolute;
  left: -5px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 0;
  border-top: 5px solid transparent;
  border-bottom: 5px solid transparent;
  border-right: 5px solid rgba(22, 25, 22, 0.9);
}

.social-icon:hover .tooltip {
  opacity: 1;
  visibility: visible;
  left: 65px;
}

/* Main Content - Force l'empilement vertical */
.main-content {
  padding-top: 0;
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 2;
  /* SUPPRIMÉ: margin-left: 80px; */
}

/* Container pour chaque section avec position relative */
.section-container {
  position: relative;
  width: 100%;
}

/* S'assurer que les composants prennent toute la largeur */
.main-content > div {
  width: 100%;
  flex-shrink: 0;
}

/* Correction pour centrer le contenu Home */
#home {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}

/* Particles Background */
.particles {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

/* Blur Background for Home Section - Émeraude en haut à gauche */
.blur-bg-home {
  position: absolute;
  top: 10%;
  left: 10%;
  width: 400px;
  height: 400px;
  background: radial-gradient(
    circle,
    rgba(80, 200, 120, 0.3) 0%,
    rgba(20, 160, 133, 0.2) 30%,
    rgba(80, 200, 120, 0.08) 60%,
    rgba(80, 200, 120, 0) 85%
  );
  filter: blur(50px);
  pointer-events: none;
  z-index: 0;
  animation: float 15s ease-in-out infinite;
  opacity: 0.6;
}

/* Animation subtile de flottement */
@keyframes float {
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(-15px, 10px) scale(1.02);
  }
  66% {
    transform: translate(10px, -5px) scale(0.98);
  }
}

.particle {
  position: absolute;
  width: 2px;
  height: 2px;
  background: rgba(80, 200, 120, 0.5);
  border-radius: 50%;
  animation: twinkle 3s infinite;
}

@keyframes twinkle {
  0%,
  100% {
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
}

/* Common Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes bounce {
  0%,
  20%,
  50%,
  80%,
  100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-10px);
  }
  60% {
    transform: translateX(-50%) translateY(-5px);
  }
}

/* Responsive */
@media (max-width: 1200px) {
  .social-sidebar {
    left: 20px;
  }
}

@media (max-width: 968px) {
  .social-sidebar {
    left: 15px;
  }

  .social-icon {
    width: 40px;
    height: 40px;
  }

  .social-icon .icon {
    width: 20px;
    height: 20px;
  }

  .blur-bg-home {
    top: 15%;
    left: 5%;
    width: 300px;
    height: 300px;
    filter: blur(40px);
  }
}

@media (max-width: 768px) {
  #app {
    padding: 10px;
  }

  .social-sidebar {
    display: none; /* Cacher sur mobile */
  }

  .blur-bg-home {
    top: 20%;
    left: 5%;
    width: 250px;
    height: 250px;
    filter: blur(30px);
    opacity: 0.5;
  }

  .particle {
    width: 1.5px;
    height: 1.5px;
    background: rgba(80, 200, 120, 0.4);
  }
}

@media (max-width: 480px) {
  .blur-bg-home {
    top: 25%;
    left: 5%;
    width: 200px;
    height: 200px;
    filter: blur(25px);
    opacity: 0.4;
  }
}
</style>
