<template>
  <section class="hero" id="home">
    <div class="hero-content">
      <p class="hero-greeting">Bonjour <span class="wave">👋</span> je suis</p>
      <h1 class="hero-name">< A. Kelly Alphador /></h1>
      <div class="hero-role">
        <span ref="typedElement"></span>
        <span class="typed-cursor">|</span>
      </div>
      
      <!-- Indication de disponibilité -->
      <div class="availability-badge">
        <span class="availability-dot"></span>
        <span class="availability-text">Disponible pour des nouvelles opportunités</span>
      </div>
      
      <!-- Image avec animation de flottement -->
      <div class="hero-avatar">
        <div class="avatar-container">
          <div class="avatar-decoration">
            <span class="decoration-circle circle-1"></span>
            <span class="decoration-circle circle-2"></span>
            <span class="decoration-circle circle-3"></span>
            <span class="decoration-circle circle-4"></span>
            <span class="decoration-circle circle-5"></span>
          </div>
          <img src="@/assets/images/avatar.png" alt="Photo de Kelly Alphador" />
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
    };
  },
  mounted() {
    this.initTyped();
  },
  beforeDestroy() {
    if (this.typed) {
      this.typed.destroy();
    }
  },
  methods: {
    initTyped() {
      this.typed = new Typed(this.$refs.typedElement, {
        strings: [
          "Full-Stack Developer",
          ".NET / Vue.js",
          "Full-Stack Developer",
          ".NET / Vue.js",
          "Full-Stack Developer",
          ".NET / Vue.js",
        ],
        typeSpeed: 80,
        backSpeed: 50,
        backDelay: 2000,
        startDelay: 1000,
        loop: true,
        showCursor: false,
      });
    },
  },
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
  padding: 0 2rem;
}

.hero-content {
  text-align: center;
  max-width: 1200px;
  animation: fadeInUp 1s ease-out;
  z-index: 2;
  position: relative;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.hero-greeting {
  font-size: 2rem;
  color: #ffffff;
  font-weight: 300;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.3s forwards;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

.wave {
  display: inline-block;
  animation: wave 1.5s ease-in-out infinite;
  transform-origin: 70% 70%;
}

@keyframes wave {
  0% {
    transform: rotate(0deg);
  }
  10% {
    transform: rotate(14deg);
  }
  20% {
    transform: rotate(-8deg);
  }
  30% {
    transform: rotate(14deg);
  }
  40% {
    transform: rotate(-4deg);
  }
  50% {
    transform: rotate(10deg);
  }
  60% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(0deg);
  }
}

.hero-name {
  font-family: "Syncopate", sans-serif;
  font-weight: 600;
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 500;
  color: #50c878;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.6s forwards;
  letter-spacing: -0.02em;
  line-height: 1.1;
  margin: 0;
}

.hero-role {
  font-family: "Syncopate", sans-serif;
  font-weight: 600;
  font-size: clamp(1.5rem, 4vw, 3rem);
  color: #ffffff;
  font-weight: 400;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.9s forwards;
  min-height: 1.5em;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0.5rem;
}

/* Indication de disponibilité */
.availability-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  background: rgba(80, 200, 120, 0.1);
  border: 1px solid rgba(80, 200, 120, 0.3);
  border-radius: 50px;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1s forwards;
  margin-bottom: 1rem;
  transition: all 0.3s ease;
}

.availability-badge:hover {
  background: rgba(80, 200, 120, 0.15);
  border-color: rgba(80, 200, 120, 0.5);
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(80, 200, 120, 0.2);
}

.availability-dot {
  width: 8px;
  height: 8px;
  background: #50c878;
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 rgba(80, 200, 120, 0.7);
  }
  70% {
    box-shadow: 0 0 0 6px rgba(80, 200, 120, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(80, 200, 120, 0);
  }
}

.availability-text {
  font-size: 0.9rem;
  color: #50c878;
  font-weight: 500;
  letter-spacing: 0.5px;
}

/* Style pour l'avatar avec animation de flottement */
.hero-avatar {
  width: 200px;
  height: 200px;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.2s forwards;
  position: relative;
}

.avatar-container {
  position: relative;
  width: 100%;
  height: 100%;
  animation: float 3s ease-in-out infinite;
}

.avatar-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  position: relative;
  z-index: 2;
}

/* Animation de flottement vertical */
@keyframes float {
  0% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-15px);
  }
  100% {
    transform: translateY(0px);
  }
}

/* Décoration autour de l'image */
.avatar-decoration {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 110%;
  height: 110%;
  z-index: 1;
}

.decoration-circle {
  position: absolute;
  border-radius: 50%;
  background: transparent;
  border: 1px solid rgba(80, 200, 120, 0.3);
  animation: pulse 4s ease-in-out infinite;
}

.circle-1 {
  top: 5%;
  left: 5%;
  width: 90%;
  height: 90%;
  animation-delay: 0s;
}

.circle-2 {
  top: 10%;
  left: 10%;
  width: 80%;
  height: 80%;
  border-color: rgba(80, 200, 120, 0.2);
  animation-delay: 0.5s;
}

.circle-3 {
  top: 15%;
  left: 15%;
  width: 70%;
  height: 70%;
  border-color: rgba(80, 200, 120, 0.15);
  animation-delay: 1s;
}

.circle-4 {
  top: 20%;
  left: 20%;
  width: 60%;
  height: 60%;
  border-color: rgba(80, 200, 120, 0.1);
  animation-delay: 1.5s;
}

.circle-5 {
  top: 25%;
  left: 25%;
  width: 50%;
  height: 50%;
  border-color: rgba(80, 200, 120, 0.05);
  animation-delay: 2s;
}

/* Curseur personnalisé pour l'animation de typing */
.typed-cursor {
  font-weight: 100;
  color: #14a085;
  animation: blink 1s infinite;
  margin-left: 4px;
}

@keyframes blink {
  0%,
  50% {
    opacity: 1;
  }
  51%,
  100% {
    opacity: 0;
  }
}

/* Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive */
@media (max-width: 968px) {
  .hero {
    padding: 0 1.5rem;
  }

  .hero-greeting {
    font-size: 1.5rem;
  }

  .hero-name {
    font-size: clamp(1.8rem, 3.5vw, 2.5rem);
  }

  .hero-avatar {
    width: 150px;
    height: 150px;
    margin-top: 0.5rem;
  }

  .hero-role {
    font-size: clamp(1.2rem, 3vw, 2rem);
  }
  
  .availability-badge {
    padding: 0.4rem 0.8rem;
  }
  
  .availability-text {
    font-size: 0.8rem;
  }
}

@media (max-width: 768px) {
  .hero {
    min-height: calc(100vh - 80px);
    padding: 2rem 1rem;
  }

  .hero-greeting {
    font-size: 1.2rem;
  }

  .hero-name {
    font-size: clamp(1.5rem, 3vw, 2rem);
  }

  .hero-avatar {
    width: 120px;
    height: 120px;
  }

  .hero-role {
    font-size: clamp(1rem, 2.5vw, 1.5rem);
  }
  
  .availability-badge {
    padding: 0.3rem 0.7rem;
    margin-bottom: 0.8rem;
  }
  
  .availability-text {
    font-size: 0.75rem;
  }
  
  /* Ajustement de l'animation sur mobile */
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
}

@media (max-width: 480px) {
  .hero {
    padding: 1rem 0.5rem;
  }

  .hero-greeting {
    font-size: 1rem;
  }

  .hero-name {
    font-size: clamp(1.3rem, 2.5vw, 1.8rem);
  }

  .hero-avatar {
    width: 100px;
    height: 100px;
  }

  .hero-role {
    font-size: clamp(0.9rem, 2vw, 1.2rem);
  }
  
  .availability-badge {
    padding: 0.25rem 0.6rem;
    margin-bottom: 0.5rem;
  }
  
  .availability-text {
    font-size: 0.7rem;
  }
}
</style>