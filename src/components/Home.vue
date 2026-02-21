<template>
  <section class="hero" id="home">
    <div class="hero-content">
      <!-- Particules décoratives -->
      <div class="hero-particles">
        <div v-for="n in 15" :key="n" class="particle" :style="getParticleStyle(n)"></div>
      </div>

      <!-- Greeting avec animation de vague améliorée -->
      <p class="hero-greeting" :class="{ 'visible': isVisible }">
        <span class="greeting-text">Bonjour</span>
        <span class="wave" @mouseenter="intensifyWave">👋</span>
        <span class="greeting-text">je suis</span>
      </p>

      <!-- Nom avec effet de révélation -->
      <h1 class="hero-name" :class="{ 'visible': isVisible }">
        <span class="name-bracket"><</span>
        <span class="name-content">
          <span class="name-letter" v-for="(letter, index) in nameLetters" 
                :key="index"
                :style="{ animationDelay: `${index * 0.05 + 0.8}s` }">
            {{ letter }}
          </span>
        </span>
        <span class="name-bracket"> /></span>
      </h1>

      <!-- Rôle avec animation typing améliorée -->
      <div class="hero-role-container" :class="{ 'visible': isVisible }">
        <div class="hero-role">
          <span ref="typedElement"></span>
          <span class="typed-cursor">|</span>
        </div>
        <div class="role-glow"></div>
      </div>
      
      <!-- Image avec animation de flottement améliorée - SANS LES ÉLÉMENTS AUTOUR -->
      <div class="hero-avatar" :class="{ 'visible': isVisible }">
        <div class="avatar-wrapper">
          <!-- Image uniquement - plus de cercles, points ou anneaux -->
          <div class="avatar-container">
            <div class="avatar-shine"></div>
            <img src="@/assets/images/avatar.png" alt="Photo de Kelly Alphador" />
          </div>
        </div>
      </div>

      <!-- Indicateur de scroll -->
      <div class="scroll-indicator" :class="{ 'visible': isVisible }">
        <span class="scroll-text">Scroll</span>
        <div class="scroll-line">
          <div class="scroll-dot"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Typed from "typed.js";

export default {
  name: "Home",
  data() {
    return {
      typed: null,
      isVisible: false,
      nameLetters: [],
      particleStyles: []
    };
  },
  mounted() {
    this.nameLetters = "A. Kelly Alphador".split('');
    this.initTyped();
    this.animateEntrance();
    this.initParticles();
  },
  beforeDestroy() {
    if (this.typed) {
      this.typed.destroy();
    }
  },
  methods: {
    initTyped() {
      setTimeout(() => {
        this.typed = new Typed(this.$refs.typedElement, {
          strings: [
            "Full-Stack Developer",
            ".NET / Vue.js",
            "Full-Stack Developer",
            ".NET / Vue.js",
            "Full-Stack Developer",
            ".NET / Vue.js",
          ],
          typeSpeed: 60,
          backSpeed: 30,
          backDelay: 2500,
          startDelay: 2000,
          loop: true,
          showCursor: false,
          smartBackspace: true
        });
      }, 1500);
    },
    animateEntrance() {
      setTimeout(() => {
        this.isVisible = true;
      }, 100);
    },
    getParticleStyle(index) {
      const size = Math.random() * 4 + 1; // Plus petites
      const duration = Math.random() * 15 + 15; // Plus lentes
      const delay = Math.random() * 5;
      const left = Math.random() * 100;
      const top = Math.random() * 100;
      
      return {
        width: `${size}px`,
        height: `${size}px`,
        left: `${left}%`,
        top: `${top}%`,
        animation: `floatParticle ${duration}s linear infinite`,
        animationDelay: `${delay}s`,
        opacity: Math.random() * 0.2 + 0.05 // Plus subtil
      };
    },
    initParticles() {
      this.particleStyles = Array(15).fill().map((_, i) => this.getParticleStyle(i));
    },
    intensifyWave() {
      const wave = document.querySelector('.wave');
      wave.style.animation = 'none';
      wave.offsetHeight;
      wave.style.animation = 'intenseWave 0.5s ease-in-out';
      setTimeout(() => {
        wave.style.animation = 'wave 2s ease-in-out infinite';
      }, 500);
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Syncopate:wght@400;500;700&display=swap");

/* Hero Section */
.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  position: relative;
  padding: 2rem 1rem;
  overflow: hidden;
  background: transparent;
}

.hero::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80vw;
  height: 80vw;
  max-width: 800px;
  max-height: 800px;
  background: radial-gradient(circle, rgba(80, 200, 120, 0.15) 0%, transparent 70%);
  border-radius: 50%;
  z-index: 0;
  pointer-events: none;
}

.hero-content {
  text-align: center;
  max-width: 1200px;
  z-index: 2;
  position: relative;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

/* Particules d'arrière-plan - plus subtiles */
.hero-particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.particle {
  position: absolute;
  background: rgba(80, 200, 120, 0.3);
  border-radius: 50%;
  pointer-events: none;
}

@keyframes floatParticle {
  0% {
    transform: translateY(0) translateX(0);
  }
  33% {
    transform: translateY(-15px) translateX(10px);
  }
  66% {
    transform: translateY(10px) translateX(-10px);
  }
  100% {
    transform: translateY(0) translateX(0);
  }
}

.hero-greeting {
  font-size: clamp(1.5rem, 5vw, 2.5rem);
  color: #ffffff;
  font-weight: 300;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  flex-wrap: wrap;
  margin-bottom: 0.5rem;
}

.hero-greeting.visible {
  opacity: 1;
  transform: translateY(0);
}

.greeting-text {
  background: linear-gradient(135deg, #ffffff, #e0e0e0);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.wave {
  display: inline-block;
  animation: wave 2s ease-in-out infinite;
  transform-origin: 70% 70%;
  font-size: clamp(2rem, 6vw, 3rem);
  cursor: default;
  transition: transform 0.3s ease;
}

.wave:hover {
  transform: scale(1.2);
}

@keyframes wave {
  0% { transform: rotate(0deg); }
  10% { transform: rotate(14deg); }
  20% { transform: rotate(-8deg); }
  30% { transform: rotate(14deg); }
  40% { transform: rotate(-4deg); }
  50% { transform: rotate(10deg); }
  60% { transform: rotate(0deg); }
  100% { transform: rotate(0deg); }
}

@keyframes intenseWave {
  0% { transform: rotate(0deg) scale(1); }
  25% { transform: rotate(20deg) scale(1.3); }
  50% { transform: rotate(-15deg) scale(1.2); }
  75% { transform: rotate(10deg) scale(1.1); }
  100% { transform: rotate(0deg) scale(1); }
}

.hero-name {
  font-family: "Syncopate", sans-serif;
  font-size: clamp(1.8rem, 6vw, 3.5rem);
  color: #50c878;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.8s ease 0.4s, transform 0.8s ease 0.4s;
  letter-spacing: -0.02em;
  line-height: 1.2;
  margin: 0.5rem 0;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.1rem;
  flex-wrap: wrap;
  width: 100%;
}

.hero-name.visible {
  opacity: 1;
  transform: translateY(0);
}

.name-bracket {
  color: rgba(80, 200, 120, 0.5);
  font-weight: 300;
  animation: glow 2s ease-in-out infinite;
  font-size: clamp(1.5rem, 5vw, 3rem);
}

.name-content {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.05rem;
}

.name-letter {
  display: inline-block;
  animation: letterPop 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform: scale(0);
  opacity: 0;
  font-size: inherit;
}

@keyframes letterPop {
  0% {
    transform: scale(0) translateY(20px);
    opacity: 0;
  }
  100% {
    transform: scale(1) translateY(0);
    opacity: 1;
  }
}

@keyframes glow {
  0%, 100% {
    text-shadow: 0 0 10px rgba(80, 200, 120, 0.3);
  }
  50% {
    text-shadow: 0 0 20px rgba(80, 200, 120, 0.8);
  }
}

/* Conteneur du rôle */
.hero-role-container {
  position: relative;
  margin: 0.5rem 0;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) 0.6s;
  width: 100%;
}

.hero-role-container.visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-role {
  font-family: "Syncopate", sans-serif;
  font-size: clamp(1.2rem, 4vw, 2.5rem);
  color: #ffffff;
  font-weight: 400;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 2;
  flex-wrap: wrap;
  padding: 0 0.5rem;
}

.role-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  background: radial-gradient(circle, rgba(80, 200, 120, 0.15) 0%, transparent 70%);
  filter: blur(15px);
  z-index: 1;
  animation: pulseGlow 3s ease-in-out infinite;
}

@keyframes pulseGlow {
  0%, 100% {
    opacity: 0.2;
    transform: translate(-50%, -50%) scale(0.8);
  }
  50% {
    opacity: 0.5;
    transform: translate(-50%, -50%) scale(1.2);
  }
}

/* Avatar simplifié - sans éléments autour */
.hero-avatar {
  width: min(200px, 40vw);
  height: min(200px, 40vw);
  opacity: 0;
  transform: translateY(30px) scale(0.9);
  transition: all 1s cubic-bezier(0.34, 1.56, 0.64, 1) 0.8s;
  position: relative;
  margin: 1rem 0;
}

.hero-avatar.visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.avatar-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
  animation: float 4s ease-in-out infinite;
}

/* Conteneur de l'image - simplifié */
.avatar-container {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  overflow: hidden;
  z-index: 2;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  border: 2px solid rgba(80, 200, 120, 0.3);
}

.avatar-shine {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  transform: rotate(45deg);
  animation: shine 4s infinite;
  z-index: 3;
  pointer-events: none;
}

@keyframes shine {
  0% {
    transform: translateX(-100%) rotate(45deg);
  }
  20%, 100% {
    transform: translateX(100%) rotate(45deg);
  }
}

.avatar-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.avatar-wrapper:hover img {
  transform: scale(1.1);
}

/* Animation de flottement */
@keyframes float {
  0% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
  100% {
    transform: translateY(0px);
  }
}

/* Indicateur de scroll */
.scroll-indicator {
  position: absolute;
  bottom: -60px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  opacity: 0;
  transition: opacity 0.8s ease 1.2s, bottom 0.8s ease 1.2s;
}

.scroll-indicator.visible {
  opacity: 1;
  bottom: -30px;
}

.scroll-text {
  font-size: 0.7rem;
  color: rgba(255, 255, 255, 0.4);
  letter-spacing: 2px;
  text-transform: uppercase;
  writing-mode: vertical-rl;
}

.scroll-line {
  width: 1px;
  height: 40px;
  background: linear-gradient(to bottom, transparent, #50c878, transparent);
  position: relative;
  overflow: hidden;
}

.scroll-dot {
  position: absolute;
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 3px;
  height: 3px;
  background: #50c878;
  border-radius: 50%;
  animation: scrollDot 1.5s ease-in-out infinite;
}

@keyframes scrollDot {
  0% {
    top: -10px;
  }
  100% {
    top: 40px;
  }
}

/* Curseur typing */
.typed-cursor {
  font-weight: 100;
  color: #50c878;
  animation: blink 1s infinite;
  margin-left: 4px;
  font-size: inherit;
}

@keyframes blink {
  0%, 50% {
    opacity: 1;
  }
  51%, 100% {
    opacity: 0;
  }
}

/* Media Queries pour un responsive parfait */
@media (max-width: 768px) {
  .hero {
    min-height: calc(100vh - 70px);
    padding: 1.5rem 1rem;
  }

  .hero-greeting {
    gap: 0.3rem;
    margin-bottom: 0.2rem;
  }

  .hero-name {
    margin: 0.2rem 0;
  }

  .hero-role-container {
    margin: 0.2rem 0;
  }

  .hero-avatar {
    margin: 0.5rem 0;
  }

  .scroll-indicator.visible {
    bottom: -20px;
  }
  
  .scroll-line {
    height: 30px;
  }
  
  @keyframes scrollDot {
    0% { top: -10px; }
    100% { top: 30px; }
  }
}

@media (max-width: 480px) {
  .hero {
    padding: 1rem 0.75rem;
    min-height: calc(100vh - 60px);
  }

  .hero-greeting {
    font-size: clamp(1.2rem, 5vw, 1.5rem);
  }

  .wave {
    font-size: clamp(1.5rem, 6vw, 2rem);
  }

  .hero-name {
    font-size: clamp(1.3rem, 5vw, 1.8rem);
  }

  .name-bracket {
    font-size: clamp(1.1rem, 4vw, 1.5rem);
  }

  .hero-role {
    font-size: clamp(1rem, 4vw, 1.3rem);
  }

  .hero-avatar {
    width: min(150px, 35vw);
    height: min(150px, 35vw);
  }

  .scroll-indicator.visible {
    bottom: -15px;
  }
  
  .scroll-text {
    font-size: 0.6rem;
  }
  
  .scroll-line {
    height: 25px;
  }
  
  @keyframes scrollDot {
    0% { top: -8px; }
    100% { top: 25px; }
  }
}

/* Pour très petits écrans */
@media (max-width: 360px) {
  .hero-greeting {
    font-size: 1rem;
  }

  .wave {
    font-size: 1.3rem;
  }

  .hero-name {
    font-size: 1.1rem;
  }

  .hero-role {
    font-size: 0.9rem;
  }

  .hero-avatar {
    width: 120px;
    height: 120px;
  }
}

/* Pour les écrans moyens */
@media (min-width: 769px) and (max-width: 1024px) {
  .hero-avatar {
    width: 180px;
    height: 180px;
  }
  
  .hero-name {
    font-size: clamp(2rem, 5vw, 3rem);
  }
  
  .hero-role {
    font-size: clamp(1.5rem, 3.5vw, 2.2rem);
  }
}

/* Pour les grands écrans */
@media (min-width: 1400px) {
  .hero-avatar {
    width: 220px;
    height: 220px;
  }
  
  .hero::before {
    width: 1000px;
    height: 1000px;
  }
}
</style>