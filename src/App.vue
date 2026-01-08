// App.vue
<template>
  <div id="app">
    <!-- Navigation -->
    <nav class="navbar" :class="{ 'scrolled': isScrolled }">
      <div class="nav-container">
        <router-link to="#" class="logo">KA</router-link>
        
        <!-- Bouton hamburger pour mobile -->
        <button class="hamburger" :class="{ 'active': isMobileMenuOpen }" @click="toggleMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>
        
        <ul class="nav-links" :class="{ 'mobile-open': isMobileMenuOpen }">
          <li><a @click.prevent="scrollToSection('home')" href="#home">Home</a></li>
          <li><a @click.prevent="scrollToSection('skills')" href="#skills">Skills</a></li>
          <li><a @click.prevent="scrollToSection('experience')" href="#experience">Experience</a></li>
          <li><a @click.prevent="scrollToSection('projects')" href="#projects">Projects</a></li>
          <li><a @click.prevent="scrollToSection('contact')" href="#contact">Contact</a></li>
        </ul>
      </div>
    </nav>
    
    <!-- Overlay pour fermer le menu en cliquant à l'extérieur -->
    <div class="overlay" :class="{ 'active': isMobileMenuOpen }" @click="toggleMobileMenu" v-if="false"></div>
    
    <!-- Main Content Container -->
    <div class="main-content">
      <div id="home">
        <Home />
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
import Home from './components/Home.vue'
import Skills from './components/Skills.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'

export default {
  name: 'App',
  components: {
    Home,
    Skills,
    Experience,
    Projects,
    Contact
  },
  data() {
    return {
      isScrolled: false,
      isMobileMenuOpen: false
    }
  },
  mounted() {
    this.createParticles()
    this.handleScroll()
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 100
    },
    scrollToSection(sectionId) {
      const element = document.getElementById(sectionId)
      if (element) {
        // Calculer la position avec un offset pour la navbar fixe
        const navbarHeight = 80
        const elementPosition = element.getBoundingClientRect().top + window.pageYOffset
        const offsetPosition = elementPosition - navbarHeight

        window.scrollTo({
          top: offsetPosition,
          behavior: 'smooth'
        })
        
        // Fermer le menu mobile après navigation
        this.isMobileMenuOpen = false
      }
    },
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen
    },
    createParticles() {
      const particlesContainer = this.$refs.particles
      const particleCount = 50

      for (let i = 0; i < particleCount; i++) {
        const particle = document.createElement('div')
        particle.className = 'particle'
        particle.style.left = Math.random() * 100 + '%'
        particle.style.top = Math.random() * 100 + '%'
        particle.style.animationDelay = Math.random() * 3 + 's'
        particlesContainer.appendChild(particle)
      }
    }
  }
}
</script>

<style>
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
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: #002C54;
  
  min-height: 100vh;
  overflow-x: hidden;
  color: #ffffff;
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

/* Main Content - Force l'empilement vertical */
.main-content {
  padding-top: 0;
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 1;
}

/* S'assurer que les composants prennent toute la largeur */
.main-content > div {
  width: 100%;
  flex-shrink: 0;
}

/* Navbar */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;
  background:rgb(0 0 0 / 10%);
  backdrop-filter: blur(10px);
  z-index: 1000;
  padding: 1rem 2rem;
  transition: all 0.3s ease;
  height: 80px;
  display: flex;
  align-items: center;
}

.navbar.scrolled {
  background: rgb(0 0 0 / 30%);
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.logo {
  font-size: 2rem;
  font-weight: bold;
  background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-decoration: none;
  transition: transform 0.3s ease;
  z-index: 1001;
}

.logo:hover {
  transform: scale(1.1);
}

/* Bouton Hamburger */
.hamburger {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 24px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 1001;
}

.hamburger span {
  width: 100%;
  height: 3px;
  background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
  border-radius: 3px;
  transition: all 0.3s ease;
}

.hamburger.active span:nth-child(1) {
  transform: rotate(45deg) translate(8px, 8px);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -7px);
}

/* Overlay pour mobile */
.overlay {
  display: none;
}

/* Navigation Links */
.nav-links {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-links a {
  color: #ffffff;
  text-decoration: none;
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
  padding: 0.5rem 1rem;
  cursor: pointer;
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 0;
  height: 2px;
  background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
  transition: all 0.3s ease;
  transform: translateX(-50%);
}

.nav-links a:hover::after {
  width: 100%;
}

.nav-links a:hover {
  transform: translateY(-2px);
}

/* Particles Background */
.particles {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.particle {
  position: absolute;
  width: 2px;
  height: 2px;
  background: rgba(78, 205, 196, 0.5);
  border-radius: 50%;
  animation: twinkle 3s infinite;
}

@keyframes twinkle {
  0%, 100% { opacity: 0; }
  50% { opacity: 1; }
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

@keyframes float {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
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
@media (max-width: 768px) {
  .navbar {
    padding: 1rem;
    height: 70px;
  }
  
  /* Afficher le bouton hamburger sur mobile */
  .hamburger {
    display: flex;
  }
  
  /* Menu mobile */
  .nav-links {
    position: absolute;
    top: 70px;
    left: 0;
    right: 0;
    width: 100%;
    max-height: 0;
    background: linear-gradient(180deg, rgba(13, 13, 13, 0.98) 0%, rgba(27, 0, 58, 0.98) 100%);
    backdrop-filter: blur(20px);
    flex-direction: column;
    padding: 0;
    gap: 0;
    overflow: hidden;
    transition: max-height 0.4s ease, padding 0.4s ease;
    border-bottom: 3px solid transparent;
    box-shadow: 0 10px 30px rgba(106, 13, 173, 0);
    z-index: 999;
  }
  
  .nav-links.mobile-open {
    max-height: 400px;
    padding: 1.5rem 0;
    border-bottom: 3px solid rgba(166, 76, 166, 0.6);
    box-shadow: 0 10px 30px rgba(106, 13, 173, 0.5);
  }
  
  .nav-links li {
    width: 100%;
    text-align: center;
    padding: 0;
    opacity: 0;
    transform: translateY(-20px);
    transition: all 0.3s ease;
  }
  
  .nav-links.mobile-open li {
    opacity: 1;
    transform: translateY(0);
  }
  
  .nav-links.mobile-open li:nth-child(1) { transition-delay: 0.1s; }
  .nav-links.mobile-open li:nth-child(2) { transition-delay: 0.15s; }
  .nav-links.mobile-open li:nth-child(3) { transition-delay: 0.2s; }
  .nav-links.mobile-open li:nth-child(4) { transition-delay: 0.25s; }
  .nav-links.mobile-open li:nth-child(5) { transition-delay: 0.3s; }
  
  .nav-links a {
    font-size: 1.1rem;
    padding: 1rem 2rem;
    display: block;
    width: 100%;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  
  .nav-links a::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, rgba(255, 110, 199, 0.2), rgba(166, 76, 166, 0.3), rgba(106, 13, 173, 0.2));
    transition: left 0.4s ease;
    z-index: -1;
  }
  
  .nav-links a::after {
    display: none;
  }
  
  .nav-links a:hover::before {
    left: 0;
  }
  
  .nav-links a:hover {
    color: #ff6ec7;
    transform: scale(1.05);
    text-shadow: 0 0 10px rgba(255, 110, 199, 0.5);
  }
}

/* Pour les très petits écrans */
@media (max-width: 480px) {
  .nav-links {
    width: 85%;
  }
  
  .logo {
    font-size: 1.5rem;
  }
}
</style>