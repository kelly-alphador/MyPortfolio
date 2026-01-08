<template>
  <div id="app">
    <!-- Navigation Bar -->
    <nav class="navbar">
      <div class="nav-container">
        <!-- Logo AKA -->
        <div class="logo">
          <span class="logo-text">AKA</span>
        </div>

        <!-- Navigation Links -->
        <div class="nav-links" :class="{ 'mobile-open': isMobileMenuOpen }">
          <a href="#home" class="nav-link" @click="closeMobileMenu">Accueil</a>
          <a href="#about" class="nav-link" @click="closeMobileMenu">À propos</a>
          <a href="#skills" class="nav-link" @click="closeMobileMenu">Compétences</a>
          <a href="#experience" class="nav-link" @click="closeMobileMenu">Expérience</a>
          <a href="#projects" class="nav-link" @click="closeMobileMenu">Projets</a>
          <a href="#contact" class="nav-link" @click="closeMobileMenu">Contact</a>
        </div>

        <!-- Download CV Button -->
        <a 
          href="/path-to-cv.pdf" 
          class="download-btn"
          download
        >
          Télécharger CV
        </a>

        <!-- Mobile Menu Toggle -->
        <button 
          class="mobile-toggle" 
          @click="toggleMobileMenu"
          aria-label="Toggle menu"
        >
          <div class="hamburger" :class="{ 'active': isMobileMenuOpen }">
            <span></span>
            <span></span>
            <span></span>
          </div>
        </button>
      </div>
    </nav>

    <!-- Active Link Indicator (mobile) -->
    <div 
      class="active-indicator" 
      :style="activeIndicatorStyle"
    ></div>

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
  data() {
    return {
      isMobileMenuOpen: false,
      activeSection: 'home',
      sections: ['home', 'about', 'skills', 'experience', 'projects', 'contact']
    };
  },
  computed: {
    activeIndicatorStyle() {
      const index = this.sections.indexOf(this.activeSection);
      if (index === -1) return { display: 'none' };
      
      return {
        left: `${index * 16.666}%`,
        width: '16.666%'
      };
    }
  },
  mounted() {
    this.createParticles();
    this.setupScrollSpy();
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
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
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen;
    },
    closeMobileMenu() {
      this.isMobileMenuOpen = false;
    },
    setupScrollSpy() {
      const observerOptions = {
        root: null,
        rootMargin: '-50% 0px -50% 0px',
        threshold: 0
      };

      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            this.activeSection = entry.target.id;
          }
        });
      }, observerOptions);

      this.sections.forEach(sectionId => {
        const section = document.getElementById(sectionId);
        if (section) {
          observer.observe(section);
        }
      });
    },
    handleResize() {
      if (window.innerWidth > 768) {
        this.isMobileMenuOpen = false;
      }
    }
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
  --nav-bg: rgba(22, 25, 22, 0.95);
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
  padding-top: 80px; /* Pour éviter que le contenu soit caché sous la navbar */
}

/* App Container */
#app {
  position: relative;
  width: 100%;
  min-height: 100vh;
  padding: 20px;
}

/* Navigation Bar */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: var(--nav-bg);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(80, 200, 120, 0.1);
  z-index: 1000;
  padding: 0 20px;
}

.nav-container {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 80px;
  position: relative;
}

/* Logo */
.logo {
  display: flex;
  align-items: center;
}

.logo-text {
  font-size: 2rem;
  font-weight: 700;
  background: linear-gradient(135deg, var(--emerald-primary), var(--emerald-dark));
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  letter-spacing: 1px;
  transition: transform 0.3s ease;
}

.logo:hover .logo-text {
  transform: scale(1.05);
}

/* Navigation Links */
.nav-links {
  display: flex;
  gap: 40px;
  align-items: center;
}

.nav-link {
  position: relative;
  color: var(--text-secondary);
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 500;
  padding: 8px 0;
  transition: color 0.3s ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--emerald-primary);
  transition: width 0.3s ease;
}

.nav-link:hover {
  /*color: var(--emerald-primary);*/
}

.nav-link:hover::after {
  width: 100%;
}

/* Active Link */
.nav-link.active {
  color: var(--emerald-primary);
}

.nav-link.active::after {
  width: 100%;
}

/* Download CV Button */
.download-btn {
  padding: 12px 28px;
  background: linear-gradient(135deg, var(--emerald-primary), var(--emerald-dark));
  color: var(--bg-dark);
  text-decoration: none;
  border-radius: 8px;
  font-weight: 600;
  font-size: 1rem;
  transition: all 0.3s ease;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  white-space: nowrap;
}

.download-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(80, 200, 120, 0.3);
}

/* Mobile Toggle */
.mobile-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  z-index: 1001;
}

.hamburger {
  display: flex;
  flex-direction: column;
  gap: 4px;
  width: 24px;
  height: 18px;
  position: relative;
}

.hamburger span {
  display: block;
  width: 100%;
  height: 2px;
  background: var(--emerald-primary);
  border-radius: 2px;
  transition: all 0.3s ease;
}

.hamburger.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -6px);
}

/* Active Indicator for Mobile */
.active-indicator {
  position: absolute;
  bottom: 0;
  height: 2px;
  background: var(--emerald-primary);
  transition: left 0.3s ease, width 0.3s ease;
  display: none;
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

/* Main Content */
.main-content {
  padding-top: 0;
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 2;
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

/* Blur Background for Home Section */
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

/* Responsive */
@media (max-width: 1200px) {
  .social-sidebar {
    left: 20px;
  }
  
  .nav-links {
    gap: 30px;
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
  
  .nav-links {
    gap: 20px;
  }
}

@media (max-width: 768px) {
  body {
    padding-top: 70px;
  }
  
  #app {
    padding: 10px;
  }

  .navbar {
    padding: 0 15px;
  }

  .nav-container {
    height: 70px;
  }

  .logo-text {
    font-size: 1.8rem;
  }

  .mobile-toggle {
    display: block;
  }

  .nav-links {
    position: fixed;
    top: 70px;
    left: 0;
    width: 100%;
    background: var(--nav-bg);
    backdrop-filter: blur(10px);
    flex-direction: column;
    gap: 0;
    padding: 20px 0;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
    border-bottom: 1px solid rgba(80, 200, 120, 0.1);
  }

  .nav-links.mobile-open {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }

  .nav-link {
    width: 100%;
    text-align: center;
    padding: 15px 20px;
    font-size: 1.2rem;
  }

  .nav-link::after {
    display: none;
  }

  .download-btn {
    position: absolute;
    right: 60px;
    padding: 10px 20px;
    font-size: 0.9rem;
  }

  .social-sidebar {
    display: none;
  }

  .active-indicator {
    display: block;
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
  body {
    padding-top: 60px;
  }
  
  .nav-container {
    height: 60px;
  }
  
  .nav-links {
    top: 60px;
  }
  
  .logo-text {
    font-size: 1.5rem;
  }
  
  .download-btn {
    right: 50px;
    padding: 8px 16px;
    font-size: 0.8rem;
  }

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