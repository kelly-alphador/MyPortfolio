<template>
  <div id="app">
    <!-- Loading Screen avec effet splash -->
    <div v-if="isLoading" class="loading-screen" :class="{ 'fade-out': isFadeOut }">
      <!-- Background rempli avec gradient -->
      <div class="splash-background">
        <div class="gradient-sphere"></div>
        <div class="gradient-sphere-2"></div>
        <div class="gradient-overlay"></div>
      </div>
      
      <!-- Lettres qui tombent -->
      <div class="letters-container">
        <div 
          v-for="(letter, index) in loadingLetters" 
          :key="index"
          class="loading-letter"
          :class="[`letter-${index}`, { 'falling': isFalling[index] }]"
          :style="getLetterStyle(index)"
        >
          {{ letter }}
        </div>
      </div>
      
      <!-- Barre de progression avec effet de glow -->
      <div class="loading-progress-container">
        <div class="loading-progress" :style="{ width: loadingProgress + '%' }">
          <div class="progress-glow"></div>
        </div>
      </div>
      
      <!-- Texte de chargement -->
      <div class="loading-text" :class="{ 'visible': loadingProgress > 0 }">
        <span v-if="loadingProgress < 33">Préparation...</span>
        <span v-else-if="loadingProgress < 66">Chargement...</span>
        <span v-else-if="loadingProgress < 100">Presque prêt...</span>
        <span v-else>Bienvenue !</span>
      </div>
    </div>

    <!-- Main App Content (visible après chargement) -->
    <template v-else>
      <!-- Navigation Bar avec animation -->
      <nav class="navbar" :class="{ 'animate-in': !isLoading }">
        <div class="nav-container">
          <!-- Logo AKA avec animation -->
          <div class="logo animate-item" style="animation-delay: 0.1s">
            <span class="logo-text">AKA</span>
          </div>

          <!-- Navigation Links avec animations -->
          <div class="nav-links" :class="{ 'mobile-open': isMobileMenuOpen }">
            <a 
              v-for="(item, index) in navItems"
              :key="item.id"
              :href="`#${item.id}`" 
              class="nav-link animate-item" 
              :class="{ 'active': activeSection === item.id }"
              :style="{ animationDelay: `${0.2 + index * 0.1}s` }"
              @click.prevent="scrollToSection(item.id)"
            >
              {{ item.label }}
            </a>
          </div>

          <!-- Boutons de droite avec animations -->
          <div class="nav-right">
            <!-- Download CV Button avec texte ou icône selon appareil -->
                  <a 
            href="/cv.pdf" 
            class="download-btn"
            :class="{ 'icon-only': isMobileOrTablet }"
            :title="isMobileOrTablet ? 'Télécharger CV' : 'Télécharger mon CV'"
            download="CV_Kelly_Alphador.pdf"
            @click="downloadCV"
          >
            <svg v-if="isMobileOrTablet" class="download-icon" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M21 15V19C21 19.5304 20.7893 20.0391 20.4142 20.4142C20.0391 20.7893 19.5304 21 19 21H5C4.46957 21 3.96086 20.7893 3.58579 20.4142C3.21071 20.0391 3 19.5304 3 19V15" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              <path d="M7 10L12 15L17 10" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              <path d="M12 15V3" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <span v-else class="download-text">Télécharger CV</span>
          </a>

            <!-- Mobile Menu Toggle avec animation -->
            <button 
              class="mobile-toggle animate-item" 
              :style="{ animationDelay: '0.9s' }"
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
        </div>
      </nav>

      <!-- Active Link Indicator (mobile) -->
      <div 
        class="active-indicator" 
        :style="activeIndicatorStyle"
      ></div>

      <!-- Social Media Sidebar avec animations -->
      <div class="social-sidebar animate-sidebar">
        <div class="social-line animate-line" style="animation-delay: 1s"></div>
        <div class="social-icons">
          <a 
            v-for="(social, index) in socialLinks"
            :key="social.id"
            :href="social.href"
            :target="social.target"
            class="social-icon animate-icon"
            :class="[social.id, { 'tooltip-active': false }]"
            :style="{ animationDelay: `${1.1 + index * 0.15}s` }"
            :aria-label="social.label"
          >
            <component :is="social.icon" class="icon" />
            <span class="tooltip">{{ social.tooltip }}</span>
          </a>
        </div>
      </div>

      <!-- Main Content Container avec animations -->
      <div class="main-content animate-content" style="animation-delay: 1.2s">
        <div id="home" class="section-container">
          <!-- Blur Background for Home - seulement dans cette section -->
          <div class="blur-bg-home animate-blur"></div>
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

      <!-- Back to Top Arrow avec animation -->
      <button 
        class="back-to-top" 
        :class="{ 'visible': showBackToTop, 'animate-btt': !showBackToTop }"
        @click="scrollToTop"
        aria-label="Retour en haut"
        style="animation-delay: 1.5s"
      >
        <svg 
          class="arrow-icon" 
          width="24" 
          height="24" 
          viewBox="0 0 24 24" 
          fill="none" 
          xmlns="http://www.w3.org/2000/svg"
        >
          <path 
            d="M12 4L12 20M12 4L18 10M12 4L6 10" 
            stroke="currentColor" 
            stroke-width="2" 
            stroke-linecap="round" 
            stroke-linejoin="round"
          />
        </svg>
      </button>

      <!-- Particles Background -->
      <div class="particles" ref="particles"></div>
    </template>
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
      isLoading: true,
      isFadeOut: false,
      loadingLetters: ['A', 'K', 'A'],
      isFalling: [false, false, false],
      loadingProgress: 0,
      isMobileMenuOpen: false,
      activeSection: 'home',
      sections: ['home', 'about', 'skills', 'experience', 'projects', 'contact'],
      showBackToTop: false,
      isMobileOrTablet: false,
      navItems: [
        { id: 'home', label: 'Accueil' },
        { id: 'about', label: 'À propos' },
        { id: 'skills', label: 'Compétences' },
        { id: 'experience', label: 'Expériences' },
        { id: 'projects', label: 'Projets' },
        { id: 'contact', label: 'Contact' }
      ],
      socialLinks: [
        { 
          id: 'phone',
          icon: 'Phone',
          href: 'tel:+261345238397',
          target: '_self',
          label: 'Téléphone',
          tooltip: '+261 34 52 383 97'
        },
        { 
          id: 'email',
          icon: 'Mail',
          href: 'mailto:kellyalphador@gmail.com',
          target: '_self',
          label: 'Email',
          tooltip: 'kellyalphador@gmail.com'
        },
        { 
          id: 'github',
          icon: 'Github',
          href: 'https://github.com/kelly-alphador',
          target: '_blank',
          label: 'GitHub',
          tooltip: 'GitHub'
        },
        { 
          id: 'linkedin',
          icon: 'Linkedin',
          href: 'https://www.linkedin.com/in/kelly-alphador-990803362/',
          target: '_blank',
          label: 'LinkedIn',
          tooltip: 'LinkedIn'
        }
      ]
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
    this.startLoadingAnimation();
    this.createParticles();
    this.setupScrollSpy();
    window.addEventListener('resize', this.handleResize);
    window.addEventListener('scroll', this.handleScroll);
    this.checkDeviceType();
    this.handleResize();
    
    // Initialiser la classe active sur le premier lien
    this.updateActiveLinks();
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    startLoadingAnimation() {
      // Animation séquentielle des lettres qui tombent
      const timings = [300, 800, 1300];
      
      timings.forEach((delay, index) => {
        setTimeout(() => {
          this.isFalling[index] = true;
          
          if (index === 0) this.loadingProgress = 33;
          else if (index === 1) this.loadingProgress = 66;
          else if (index === 2) this.loadingProgress = 100;
        }, delay);
      });

      setTimeout(() => {
        this.isFadeOut = true;
        setTimeout(() => {
          this.isLoading = false;
        }, 800);
      }, 2300);
    },
    getLetterStyle(index) {
      const colors = [
        '#50c878',
        '#2e8b57',
        '#50c878'
      ];
      
      const sizes = ['8rem', '9rem', '8rem'];
      
      return {
        color: colors[index],
        fontSize: sizes[index],
        textShadow: `0 0 40px ${colors[index]}, 0 0 80px ${colors[index]}80`
      };
    },
    checkDeviceType() {
      this.isMobileOrTablet = window.innerWidth <= 1024;
    },
    createParticles() {
      const particlesContainer = this.$refs.particles;
      if (!particlesContainer) return;
      
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
            this.updateActiveLinks();
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
    updateActiveLinks() {
      this.$nextTick(() => {
        document.querySelectorAll('.nav-link').forEach(link => {
          link.classList.remove('active');
          if (link.getAttribute('href') === `#${this.activeSection}`) {
            link.classList.add('active');
          }
        });
      });
    },
    scrollToSection(sectionId) {
      this.activeSection = sectionId;
      this.updateActiveLinks();
      this.closeMobileMenu();
      
      const section = document.getElementById(sectionId);
      if (section) {
        section.scrollIntoView({ behavior: 'smooth' });
      }
    },
    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
      this.activeSection = 'home';
      this.updateActiveLinks();
    },
    downloadCV() {
      console.log('Téléchargement du CV...');
      this.closeMobileMenu();
    },
    handleScroll() {
      this.showBackToTop = window.scrollY > 500;
    },
    handleResize() {
      this.checkDeviceType();
      if (window.innerWidth > 1024) {
        this.isMobileMenuOpen = false;
      }
    }
  },
};
</script>

<style>
/* Import Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Jost:ital,wght@0,100..900;1,100..900&display=swap');

:root {
  --emerald-primary: #50c878;
  --emerald-dark: #2e8b57;
  --text-primary: #ffffff;
  --text-secondary: #e8f5e9;
  --bg-dark: #0a0c0a;
  --nav-bg: rgba(10, 12, 10, 0.95);
}

/* Animations d'ouverture */
@keyframes slideDown {
  0% {
    opacity: 0;
    transform: translateY(-100%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideUp {
  0% {
    opacity: 0;
    transform: translateY(50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideLeft {
  0% {
    opacity: 0;
    transform: translateX(-50px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes slideRight {
  0% {
    opacity: 0;
    transform: translateX(50px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInScale {
  0% {
    opacity: 0;
    transform: scale(0.8);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes rotateIn {
  0% {
    opacity: 0;
    transform: rotate(-180deg) scale(0.5);
  }
  100% {
    opacity: 1;
    transform: rotate(0) scale(1);
  }
}

@keyframes bounceIn {
  0% {
    opacity: 0;
    transform: scale(0.3);
  }
  50% {
    opacity: 1;
    transform: scale(1.05);
  }
  70% {
    transform: scale(0.9);
  }
  100% {
    transform: scale(1);
  }
}

@keyframes glowPulse {
  0% {
    opacity: 0;
    filter: blur(10px);
    transform: scale(0.9);
  }
  50% {
    opacity: 0.5;
    filter: blur(5px);
    transform: scale(1.1);
  }
  100% {
    opacity: 1;
    filter: blur(0);
    transform: scale(1);
  }
}

@keyframes lineGrow {
  0% {
    height: 0;
    opacity: 0;
  }
  100% {
    height: 100px;
    opacity: 1;
  }
}

/* Application des animations */
.navbar.animate-in {
  animation: slideDown 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

.animate-item {
  opacity: 0;
  animation: slideUp 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

.nav-link.animate-item {
  animation-name: fadeInScale;
}

.download-btn.animate-item {
  animation-name: bounceIn;
}

.mobile-toggle.animate-item {
  animation-name: rotateIn;
}

.animate-sidebar {
  opacity: 0;
  animation: slideLeft 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

.animate-line {
  opacity: 0;
  animation: lineGrow 0.6s ease-out forwards;
}

.animate-icon {
  opacity: 0;
  animation: bounceIn 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

/* Animations spécifiques pour chaque icône sociale */
.social-icon.phone.animate-icon {
  animation-name: slideLeft;
}

.social-icon.email.animate-icon {
  animation-name: slideUp;
}

.social-icon.github.animate-icon {
  animation-name: slideRight;
}

.social-icon.linkedin.animate-icon {
  animation-name: fadeInScale;
}

.animate-content {
  opacity: 0;
  animation: slideUp 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

.animate-blur {
  opacity: 0;
  animation: glowPulse 1.5s ease-out forwards;
}

.animate-btt {
  opacity: 0;
  animation: bounceIn 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

/* Loading Screen */
.loading-screen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: var(--bg-dark);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 9999;
  transition: opacity 0.8s ease-in-out, transform 0.8s ease-in-out;
}

.loading-screen.fade-out {
  opacity: 0;
  transform: scale(1.1);
  pointer-events: none;
}

.splash-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.gradient-sphere {
  position: absolute;
  top: -50%;
  left: -20%;
  width: 80%;
  height: 200%;
  background: radial-gradient(
    circle at center,
    rgba(80, 200, 120, 0.3) 0%,
    rgba(46, 139, 87, 0.2) 30%,
    transparent 70%
  );
  filter: blur(60px);
  animation: rotateSphere 20s linear infinite;
}

.gradient-sphere-2 {
  position: absolute;
  bottom: -50%;
  right: -20%;
  width: 80%;
  height: 200%;
  background: radial-gradient(
    circle at center,
    rgba(80, 200, 120, 0.25) 0%,
    rgba(20, 160, 133, 0.15) 40%,
    transparent 70%
  );
  filter: blur(60px);
  animation: rotateSphere2 25s linear infinite;
}

.gradient-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    circle at 30% 50%,
    rgba(80, 200, 120, 0.1) 0%,
    transparent 50%
  );
  pointer-events: none;
}

@keyframes rotateSphere {
  0% {
    transform: rotate(0deg) scale(1);
  }
  50% {
    transform: rotate(180deg) scale(1.2);
  }
  100% {
    transform: rotate(360deg) scale(1);
  }
}

@keyframes rotateSphere2 {
  0% {
    transform: rotate(0deg) scale(1.2);
  }
  50% {
    transform: rotate(-180deg) scale(1);
  }
  100% {
    transform: rotate(-360deg) scale(1.2);
  }
}

.letters-container {
  display: flex;
  gap: 30px;
  justify-content: center;
  align-items: center;
  margin-bottom: 60px;
  perspective: 1000px;
  z-index: 10;
  position: relative;
}

.loading-letter {
  font-family: "Jost", sans-serif;
  font-weight: 800;
  opacity: 0;
  transform: translateY(-100vh) rotateX(-90deg) scale(0.5);
  transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
  position: relative;
  filter: drop-shadow(0 0 30px currentColor);
}

.loading-letter.falling {
  opacity: 1;
  transform: translateY(0) rotateX(0) scale(1);
}

@keyframes fallLetter {
  0% {
    opacity: 0;
    transform: translateY(-100vh) rotateX(-90deg) scale(0.5);
  }
  40% {
    opacity: 0.8;
    transform: translateY(30px) rotateX(15deg) scale(1.1);
  }
  60% {
    transform: translateY(-15px) rotateX(-5deg) scale(1);
  }
  80% {
    transform: translateY(5px) rotateX(2deg) scale(0.98);
  }
  100% {
    opacity: 1;
    transform: translateY(0) rotateX(0) scale(1);
  }
}

.loading-letter.falling {
  animation: fallLetter 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

.loading-progress-container {
  width: 300px;
  height: 6px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 3px;
  overflow: hidden;
  position: relative;
  z-index: 10;
  box-shadow: 0 0 20px rgba(80, 200, 120, 0.3);
}

.loading-progress {
  height: 100%;
  background: linear-gradient(90deg, var(--emerald-primary), var(--emerald-dark));
  border-radius: 3px;
  transition: width 0.3s ease;
  position: relative;
  overflow: hidden;
}

.progress-glow {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.3),
    transparent
  );
  animation: progressGlow 1.5s linear infinite;
}

@keyframes progressGlow {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}

.loading-text {
  margin-top: 30px;
  font-size: 1.2rem;
  color: var(--text-secondary);
  letter-spacing: 2px;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.5s ease;
  z-index: 10;
  position: relative;
  text-transform: uppercase;
  font-weight: 300;
}

.loading-text.visible {
  opacity: 1;
  transform: translateY(0);
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-15px) scale(1.05);
  }
}

.loading-letter.falling.letter-0 {
  animation: fallLetter 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards,
             bounce 2s ease-in-out 0.8s infinite;
}

.loading-letter.falling.letter-1 {
  animation: fallLetter 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards,
             bounce 2s ease-in-out 0.9s infinite;
}

.loading-letter.falling.letter-2 {
  animation: fallLetter 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards,
             bounce 2s ease-in-out 1s infinite;
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
  padding-top: 80px;
}

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
  opacity: 0;
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

.logo {
  display: flex;
  align-items: center;
  flex: 1;
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

.nav-links {
  display: flex;
  gap: 40px;
  align-items: center;
  justify-content: center;
  flex: 2;
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
  color: var(--emerald-primary);
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link.active {
  color: var(--emerald-primary);
}

.nav-link.active::after {
  width: 100%;
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 20px;
  flex: 1;
  justify-content: flex-end;
}

/* Download CV Button - Style amélioré */
.download-btn {
  padding: 12px 28px;
  background: linear-gradient(135deg, #33c965, var(--emerald-dark));
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
  min-width: 180px;
  gap: 10px;
  box-shadow: 0 4px 15px rgba(80, 200, 120, 0.2);
}

.download-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(80, 200, 120, 0.4);
  background: linear-gradient(135deg, #2eb85c, #267d46);
}

.download-btn:active {
  transform: translateY(0);
}

.download-text {
  display: flex;
  align-items: center;
  gap: 8px;
}

.btn-icon {
  width: 20px;
  height: 20px;
  stroke: var(--bg-dark);
}

/* Version icône seulement pour mobile/tablette */
.download-btn.icon-only {
  padding: 10px;
  min-width: auto;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 0;
}

.download-icon {
  width: 24px;
  height: 24px;
  stroke: var(--bg-dark);
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

.main-content {
  padding-top: 0;
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 2;
}

.section-container {
  position: relative;
  width: 100%;
}

.main-content > div {
  width: 100%;
  flex-shrink: 0;
}

#home {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}

.particles {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

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

/* Back to Top Arrow */
.back-to-top {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, var(--emerald-primary), var(--emerald-dark));
  border: none;
  border-radius: 50%;
  color: var(--bg-dark);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  visibility: hidden;
  transform: translateY(20px);
  transition: all 0.3s ease;
  z-index: 100;
  box-shadow: 0 4px 15px rgba(80, 200, 120, 0.3);
  animation: continuousBounce 2s ease-in-out infinite;
}

.back-to-top.visible {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.back-to-top:hover {
  transform: translateY(0) scale(1.1);
  box-shadow: 0 8px 25px rgba(80, 200, 120, 0.4);
  animation: continuousBounceFast 1s ease-in-out infinite;
}

.arrow-icon {
  transition: transform 0.3s ease;
  animation: arrowFloat 2s ease-in-out infinite;
}

.back-to-top:hover .arrow-icon {
  animation: arrowFloatFast 1s ease-in-out infinite;
}

@keyframes continuousBounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}

@keyframes continuousBounceFast {
  0%, 100% {
    transform: translateY(0) scale(1.1);
  }
  50% {
    transform: translateY(-8px) scale(1.1);
  }
}

@keyframes arrowFloat {
  0%, 100% {
    transform: translateY(0);
  }
  25% {
    transform: translateY(-2px);
  }
  50% {
    transform: translateY(0);
  }
  75% {
    transform: translateY(2px);
  }
}

@keyframes arrowFloatFast {
  0%, 100% {
    transform: translateY(0);
  }
  25% {
    transform: translateY(-3px);
  }
  50% {
    transform: translateY(0);
  }
  75% {
    transform: translateY(3px);
  }
}

/* Responsive Design */
@media (max-width: 1200px) {
  .social-sidebar {
    left: 20px;
  }
  
  .nav-links {
    gap: 30px;
  }
  
  .download-btn:not(.icon-only) {
    padding: 10px 20px;
    min-width: 160px;
    font-size: 0.95rem;
  }
}

@media (max-width: 1024px) {
  body {
    padding-top: 75px;
  }
  
  .nav-container {
    height: 75px;
  }
  
  .logo-text {
    font-size: 1.8rem;
  }
  
  .nav-links {
    gap: 0;
    position: fixed;
    top: 75px;
    left: 0;
    width: 100%;
    background: var(--nav-bg);
    backdrop-filter: blur(10px);
    flex-direction: column;
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
    font-size: 1.1rem;
  }
  
  .nav-link::after {
    display: none;
  }
  
  .nav-link.active {
    background: rgba(80, 200, 120, 0.1);
  }
  
  .mobile-toggle {
    display: block;
    order: 3;
  }
  
  .active-indicator {
    display: block;
  }
  
  .download-btn {
    min-width: auto;
    width: 50px;
    height: 50px;
    padding: 10px;
    border-radius: 50%;
    order: 2;
  }
  
  .download-text {
    display: none;
  }
  
  .download-icon {
    display: block;
  }
  
  .nav-right {
    gap: 15px;
  }
  
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
  
  .tooltip {
    font-size: 0.85rem;
    padding: 6px 10px;
  }
  
  .blur-bg-home {
    width: 350px;
    height: 350px;
    filter: blur(45px);
  }

  .loading-letter {
    font-size: 6rem !important;
  }
  
  .loading-progress-container {
    width: 250px;
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
    top: 70px;
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

  .back-to-top {
    bottom: 20px;
    right: 20px;
    width: 45px;
    height: 45px;
    animation: continuousBounceMobile 2s ease-in-out infinite;
  }
  
  @keyframes continuousBounceMobile {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-6px);
    }
  }

  .loading-letter {
    font-size: 5rem !important;
  }
  
  .letters-container {
    gap: 15px;
  }
  
  .loading-progress-container {
    width: 200px;
  }
  
  .loading-text {
    font-size: 1rem;
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
  
  .nav-right {
    gap: 10px;
  }
  
  .download-btn {
    width: 45px;
    height: 45px;
    padding: 8px;
  }
  
  .download-icon {
    width: 20px;
    height: 20px;
  }

  .blur-bg-home {
    top: 25%;
    left: 5%;
    width: 200px;
    height: 200px;
    filter: blur(25px);
    opacity: 0.4;
  }

  .back-to-top {
    bottom: 15px;
    right: 15px;
    width: 40px;
    height: 40px;
  }

  .loading-letter {
    font-size: 3.5rem !important;
  }
  
  .letters-container {
    gap: 10px;
  }
  
  .loading-progress-container {
    width: 180px;
  }
}
</style>