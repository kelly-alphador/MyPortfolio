<template>
  <section class="hero" id="home">
    <div class="floating-element" v-for="n in 3" :key="n"></div>
    
    <div class="hero-content">
      <p class="hero-subtitle">Bonjour, je suis <span class="wave">👋</span></p>
      <h1 class="hero-title">
        <span ref="typedElement"></span>
        <span class="typed-cursor">|</span>
      </h1>
      <p class="hero-description">
          Développeur Full-Stack .NET / Vue.js, passionné par la création de solutions web et desktop modernes et performantes.
          Je maîtrise ASP.NET MVC, ASP.NET Core Web API, WPF, ainsi que .NET Framework et .NET Core, et j'intègre des interfaces utilisateur modernes avec Vue.js pour transformer vos idées en applications robustes et maintenables.
      </p>
      <div class="cta-buttons">
        <a href="/cv.pdf" download class="btn btn-primary">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="download-icon">
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path>
            <polyline points="7 10 12 15 17 10"></polyline>
            <line x1="12" y1="15" x2="12" y2="3"></line>
          </svg>
          Télécharger CV
        </a>
        <a href="#contact" class="btn btn-secondary" @click="scrollToSection('contact')">Me contacter</a>
      </div>
    </div>

   
  </section>
</template>

<script>
import Typed from 'typed.js'

export default {
  name: 'Home',
  data() {
    return {
      typed: null
    }
  },
  mounted() {
    this.initTyped()
  },
  beforeDestroy() {
    if (this.typed) {
      this.typed.destroy()
    }
  },
  methods: {
    initTyped() {
      this.typed = new Typed(this.$refs.typedElement, {
        strings: [
          'Kelly Alphador',
          'Full-Stack Developer',
          '.NET / Vue.js',
           'Kelly Alphador',
          'Full-Stack Developer',
          '.NET / Vue.js',
           'Kelly Alphador',
          'Full-Stack Developer',
          '.NET / Vue.js',
          'Kelly Alphador'
        ],
        typeSpeed: 80,
        backSpeed: 50,
        backDelay: 2000,
        startDelay: 1000,
        loop: false,
        showCursor: false,
        onComplete: () => {
          // Cache le curseur personnalisé quand l'animation est terminée
          const cursor = document.querySelector('.typed-cursor')
          if (cursor) {
            cursor.style.display = 'none'
          }
        }
      })
    },
    scrollToSection(sectionId) {
      const element = document.getElementById(sectionId)
      if (element) {
        element.scrollIntoView({ behavior: 'smooth', block: 'start' })
      }
    }
  }
}
</script>

<style scoped>
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
}

.hero-subtitle {
  font-size: 1.9rem;
  color: #d767f1;
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
  0% { transform: rotate(0deg); }
  10% { transform: rotate(14deg); }
  20% { transform: rotate(-8deg); }
  30% { transform: rotate(14deg); }
  40% { transform: rotate(-4deg); }
  50% { transform: rotate(10deg); }
  60% { transform: rotate(0deg); }
  100% { transform: rotate(0deg); }
}

.hero-title {
  font-size: clamp(1rem, 9vw, 9rem);
  font-weight: 630;
  margin-bottom: 1rem;
   background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.6s forwards;
  letter-spacing: -0.02em;
  white-space: nowrap;
  text-align: center;
  width: 100%;
  min-height: 1.2em; /* Assure une hauteur constante */
  display: flex;
  align-items: center;
  justify-content: center;
  
}

/* Curseur personnalisé pour l'animation de typing */
.typed-cursor {
  font-weight: 100;
  color: #4ecdc4;
  animation: blink 1s infinite;
  margin-left: 4px;
}

@keyframes blink {
  0%, 50% {
    opacity: 1;
  }
  51%, 100% {
    opacity: 0;
  }
}

.hero-description {
  font-size: 1rem;
  color: white;
  margin-bottom: 3rem;
  line-height: 1.7;
      font-family: Monument, sans-serif;
   width: 60%;
   text-align:left;
}

.cta-buttons {
  display: flex;
  gap: 2rem;
  justify-content: center;
  flex-wrap: wrap;
  opacity: 0;
  animation: fadeInUp 1s ease-out 1.2s forwards;
}

.btn {
  padding: 1.2rem 2.5rem;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  position: relative;
  overflow: hidden;
  min-width: 180px;
  text-align: center;
}

.download-icon {
  transition: transform 0.3s ease;
}

.btn-primary {
    background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
  color: #ffffff;
  box-shadow: 0 10px 30px rgba(255, 107, 107, 0.3);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(255, 107, 107, 0.4);
}

.btn-primary:hover .download-icon {
  transform: translateY(3px);
}

.btn-secondary {
  background: transparent;
  color: #ffffff;
  border: 2px solid #d767f1;
}

.btn-secondary:hover {
  background: #d767f1;
  color: #0c0c0c;
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(255, 107, 107, 0.4);
}

/* Floating elements 
.floating-element {
  position: absolute;
  border-radius: 50%;
  background: rgba(215, 103, 241, 0.7);

  animation: float 8s ease-in-out infinite;
  backdrop-filter: blur(1px);
}*/
/* Floating elements */
.floating-element {
  position: absolute;
  border-radius: 50%;
  background: rgba(215, 103, 241, 0.7);
  animation: float 8s ease-in-out infinite;
  filter: blur(0px); /* Applique le flou à l'élément lui-même */
}
.floating-element:nth-child(1) {
  width: 120px;
  height: 120px;
  top: 15%;
  left: 8%;
  animation-delay: 0s;
}

.floating-element:nth-child(2) {
  width: 200px;
  height: 200px;
  top: 50%;
  right: 10%;
  animation-delay: 2s;
}

.floating-element:nth-child(3) {
  width: 90px;
  height: 90px;
  bottom: 25%;
  left: 15%;
  animation-delay: 4s;
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

@keyframes float {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  33% {
    transform: translateY(-15px) rotate(60deg);
  }
  66% {
    transform: translateY(-25px) rotate(120deg);
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-15px);
  }
  60% {
    transform: translateX(-50%) translateY(-8px);
  }
}

@media (max-width: 968px) {
  .hero {
    padding: 0 1.5rem;
    padding-top: 3rem;
  }

  .hero-content {
    max-width: 100%;
  }

  .hero-title {
    font-size: clamp(2.8rem, 9vw, 5rem);
    margin-bottom: 2rem;
    font-family: Monument, sans-serif;
    white-space: normal;
  }

  .hero-description {
  
   width: 100%;
  
  }

  .cta-buttons {
    gap: 1.5rem;
  }
}

@media (max-width: 768px) {
  .hero {
    min-height: calc(100vh - 80px);
    padding: 2rem 1rem;
    padding-top: 2rem;
  }

  .hero-content {
    padding: 0;
  }

  .hero-subtitle {
    font-size: 1.1rem;
    margin-bottom: 1rem;
  }

  .hero-title {
    white-space: normal;
    font-size: clamp(2.2rem, 8vw, 3.5rem);
    margin-bottom: 1.5rem;
  }

  .hero-description {
    font-size: 1.1rem;
    margin-bottom: 2rem;
  }

  .cta-buttons {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }

  .btn {
    padding: 1rem 2rem;
    width: 100%;
    max-width: 280px;
  }

  .floating-element {
    display: none;
  }

  .scroll-indicator {
    bottom: 2rem;
  }
}

@media (max-width: 480px) {
  .hero {
    padding: 1rem 0.5rem;
  }

  .hero-title {
    font-size: clamp(2rem, 7vw, 3rem);
  }

  .hero-description {
    font-size: 1rem;
    padding: 0 1rem;
    text-align:left;
  }
}
</style>