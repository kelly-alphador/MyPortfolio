<template>
  <section class="hero" id="home">
    <div class="hero-content">
      <p class="hero-greeting">Bonjour <span class="wave">👋</span> je suis</p>
      <h1 class="hero-name">< A. Kelly Alphador /></h1>
      <div class="hero-role">
        <span ref="typedElement"></span>
        <span class="typed-cursor">|</span>
      </div>
      <!-- Image ajoutée ici -->
      <div class="hero-avatar">
        <img src="@/assets/images/avatar.png" alt="Photo de Kelly Alphador" />
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
  margin-bottom: 1rem;
}

/* Style pour l'avatar - sans bordure ni ombre */
.hero-avatar {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  overflow: hidden;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.2s forwards;
  /* Bordure et ombre retirées */
}

.hero-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
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
}
</style>
