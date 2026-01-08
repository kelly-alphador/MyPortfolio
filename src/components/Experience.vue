<template>
  <section class="experience" id="experience">
    <div class="container">
      <div class="section-header" data-aos="fade-up" data-aos-duration="1000">
        <h2 class="section-title">Mon Expérience</h2>
        <p class="section-subtitle">Projets réalisés et expertise acquise</p>
      </div>
      
      <div class="experience-timeline">
        <!-- WBS Experience -->
        <div 
          class="experience-item" 
          data-aos="fade-right"
          data-aos-duration="800"
          data-aos-delay="200"
        >
          <div class="experience-card">
            <div class="experience-header">
              <div class="company-logo">
                <span class="logo-text">WBS</span>
              </div>
              <div class="experience-info">
                <h3 class="job-title">Développeur Full-Stack</h3>
                <h4 class="company-name">WBS Enterprise</h4>
                <span class="experience-duration">2023 - 2024</span>
              </div>
            </div>
            
            <div class="experience-content">
              <h5 class="project-title">Application de Gestion de Devis</h5>
              <p class="project-description">
                Développement d'une application web complète pour la gestion automatisée des devis clients. 
                Interface utilisateur moderne et intuitive avec dashboard analytique en temps réel.
              </p>
              
              <div class="tech-stack">
                <span class="tech-tag">Symfony</span>
                <span class="tech-tag">Vue.js</span>
                <span class="tech-tag">PHP</span>
                <span class="tech-tag">MySQL</span>
                <span class="tech-tag">JavaScript</span>
              </div>
              
              <div class="achievements">
                <div class="achievement">
                  <div class="achievement-icon">📈</div>
                  <span>+40% efficacité des équipes commerciales</span>
                </div>
                <div class="achievement">
                  <div class="achievement-icon">⚡</div>
                  <span>Génération automatisée des devis</span>
                </div>
                <div class="achievement">
                  <div class="achievement-icon">🎯</div>
                  <span>Interface responsive multi-plateforme</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Spray Info Experience -->
        <div 
          class="experience-item" 
          data-aos="fade-left"
          data-aos-duration="800"
          data-aos-delay="300"
        >
          <div class="experience-card">
            <div class="experience-header">
              <div class="company-logo">
                <span class="logo-text">SI</span>
              </div>
              <div class="experience-info">
                <h3 class="job-title">Développeur .NET</h3>
                <h4 class="company-name">Spray Info</h4>
                <span class="experience-duration">2022 - 2023</span>
              </div>
            </div>
            
            <div class="experience-content">
              <h5 class="project-title">Site E-commerce B2B</h5>
              <p class="project-description">
                Création d'une plateforme e-commerce robuste et sécurisée pour la vente en ligne B2B. 
                Architecture scalable avec gestion avancée des stocks et système de paiement intégré.
              </p>
              
              <div class="tech-stack">
                <span class="tech-tag">ASP.NET MVC</span>
                <span class="tech-tag">C#</span>
                <span class="tech-tag">SQL Server</span>
                <span class="tech-tag">Entity Framework</span>
                <span class="tech-tag">Bootstrap</span>
              </div>
              
              <div class="achievements">
                <div class="achievement">
                  <div class="achievement-icon">🛒</div>
                  <span>Système de commande complet</span>
                </div>
                <div class="achievement">
                  <div class="achievement-icon">💳</div>
                  <span>Intégration paiement sécurisé</span>
                </div>
                <div class="achievement">
                  <div class="achievement-icon">📊</div>
                  <span>Dashboard administrateur avancé</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import AOS from 'aos'
import 'aos/dist/aos.css'

export default {
  name: 'ExperienceSection',
  mounted() {
    // Initialiser AOS
    AOS.init({
      duration: 1000,
      easing: 'ease-out-cubic',
      once: true,
      offset: 120,
      delay: 100,
      anchorPlacement: 'top-bottom'
    })

    // Rafraîchir AOS après le montage du composant
    this.$nextTick(() => {
      AOS.refresh()
    })
  },
  beforeDestroy() {
    // Nettoyer AOS
    AOS.refreshHard()
  }
}
</script>

<style scoped>
/* Experience Section */
.experience {
    min-height: 100vh;
    padding: 8rem 1rem 4rem;
    position: relative;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
}

.section-header {
    text-align: center;
    margin-bottom: 4rem;
}

.section-title {
    font-size: clamp(2.5rem, 5vw, 4rem);
    font-weight: 800;
    margin-bottom: 1rem;
    background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.section-subtitle {
    font-size: 1.2rem;
    color: #b8b8b8;
    max-width: 600px;
    margin: 0 auto;
    padding: 0 1rem;
}

/* Timeline pour desktop */
.experience-timeline {
    max-width: 1000px;
    margin: 0 auto;
    position: relative;
}

.experience-timeline::before {
    content: '';
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    width: 4px;
    height: 100%;
    background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
    border-radius: 2px;
}

.experience-item {
    position: relative;
    margin-bottom: 4rem;
    width: 50%;
}

.experience-item:nth-child(odd) {
    left: 0;
    padding-right: 3rem;
}

.experience-item:nth-child(even) {
    left: 50%;
    padding-left: 3rem;
}

.experience-item::after {
    content: '';
    position: absolute;
    top: 2rem;
    width: 20px;
    height: 20px;
    background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
    border-radius: 50%;
    border: 4px solid #0c0c0c;
    box-shadow: 0 0 20px rgba(78, 205, 196, 0.5);
}

.experience-item:nth-child(odd)::after {
    right: -10px;
}

.experience-item:nth-child(even)::after {
    left: -10px;
}

/* Carte d'expérience */
.experience-card {
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(15px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 20px;
    padding: 2rem;
    position: relative;
    overflow: hidden;
    transition: all 0.4s ease;
}

.experience-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 25px 50px rgba(78, 205, 196, 0.15);
    border-color: rgba(78, 205, 196, 0.3);
}

/* En-tête de l'expérience */
.experience-header {
    display: flex;
    align-items: center;
    margin-bottom: 1.5rem;
    gap: 1rem;
}

.company-logo {
    width: 60px;
    height: 60px;
    background: linear-gradient(45deg, #ff6ec7, #a64ca6, #6a0dad);
    border-radius: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.logo-text {
    font-size: 1.5rem;
    font-weight: bold;
    color: #ffffff;
}

.experience-info {
    flex: 1;
}

.experience-info h3 {
    color: #ffffff;
    font-size: 1.3rem;
    font-weight: 700;
    margin-bottom: 0.3rem;
}

.company-name {
    color: #4ecdc4;
    font-size: 1.1rem;
    font-weight: 600;
    margin-bottom: 0.3rem;
}

.experience-duration {
    color: #b8b8b8;
    font-size: 0.9rem;
    background: rgba(78, 205, 196, 0.1);
    padding: 0.3rem 0.8rem;
    border-radius: 15px;
    display: inline-block;
}

/* Contenu de l'expérience */
.experience-content {
    margin-top: 1rem;
}

.project-title {
    color: #ff6b6b;
    font-size: 1.2rem;
    font-weight: 600;
    margin-bottom: 1rem;
}

.project-description {
    color: #b8b8b8;
    line-height: 1.6;
    margin-bottom: 1.5rem;
}

/* Stack technique */
.tech-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
}

.tech-tag {
    background: rgba(78, 205, 196, 0.2);
    color: #4ecdc4;
    padding: 0.4rem 0.8rem;
    border-radius: 15px;
    font-size: 0.85rem;
    font-weight: 500;
    border: 1px solid rgba(78, 205, 196, 0.3);
    transition: all 0.3s ease;
}

.tech-tag:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(78, 205, 196, 0.2);
}

/* Réalisations */
.achievements {
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
}

.achievement {
    display: flex;
    align-items: center;
    color: #b8b8b8;
    font-size: 0.9rem;
    transition: all 0.3s ease;
}

.achievement:hover {
    color: #ffffff;
    transform: translateX(5px);
}

.achievement-icon {
    margin-right: 0.8rem;
    font-size: 1.2rem;
    flex-shrink: 0;
}

/* Animations AOS */
[data-aos="fade-right"] {
    transform: translate3d(-100px, 0, 0);
    opacity: 0;
}

[data-aos="fade-left"] {
    transform: translate3d(100px, 0, 0);
    opacity: 0;
}

/* RESPONSIVE DESIGN - TÉLÉPHONE */
@media (max-width: 768px) {
    .experience {
        padding: 6rem 1rem 3rem;
    }

    .section-header {
        margin-bottom: 3rem;
    }

    .section-title {
        font-size: clamp(2rem, 8vw, 3rem);
    }

    .section-subtitle {
        font-size: 1rem;
        padding: 0 0.5rem;
    }

    /* Timeline mobile */
    .experience-timeline::before {
        left: 20px;
    }

    .experience-item {
        width: 100% !important;
        left: 0 !important;
        padding-left: 3rem !important;
        padding-right: 0 !important;
        margin-bottom: 2.5rem;
    }

    .experience-item::after {
        left: 12px !important;
        right: auto !important;
        width: 16px;
        height: 16px;
        top: 1.5rem;
    }

    /* Carte mobile */
    .experience-card {
        padding: 1.5rem;
        border-radius: 15px;
    }

    .experience-card:hover {
        transform: translateY(-5px);
    }

    /* En-tête mobile */
    .experience-header {
        flex-direction: column;
        align-items: flex-start;
        gap: 1rem;
        margin-bottom: 1rem;
    }

    .company-logo {
        width: 50px;
        height: 50px;
    }

    .logo-text {
        font-size: 1.2rem;
    }

    .experience-info h3 {
        font-size: 1.1rem;
    }

    .company-name {
        font-size: 1rem;
    }

    .experience-duration {
        font-size: 0.8rem;
        padding: 0.2rem 0.6rem;
    }

    /* Contenu mobile */
    .project-title {
        font-size: 1.1rem;
        margin-bottom: 0.8rem;
    }

    .project-description {
        font-size: 0.9rem;
        margin-bottom: 1.2rem;
    }

    /* Stack technique mobile */
    .tech-stack {
        gap: 0.4rem;
        margin-bottom: 1.2rem;
    }

    .tech-tag {
        font-size: 0.75rem;
        padding: 0.3rem 0.6rem;
    }

    /* Réalisations mobile */
    .achievements {
        gap: 0.6rem;
    }

    .achievement {
        font-size: 0.85rem;
        align-items: flex-start;
    }

    .achievement-icon {
        font-size: 1rem;
        margin-right: 0.6rem;
        margin-top: 0.1rem;
    }

    /* Ajuster les animations AOS pour mobile */
    [data-aos="fade-right"],
    [data-aos="fade-left"] {
        transform: translate3d(0, 30px, 0);
    }
}

/* Très petits écrans */
@media (max-width: 480px) {
    .experience {
        padding: 5rem 0.5rem 2rem;
    }

    .experience-item {
        padding-left: 2rem !important;
    }

    .experience-timeline::before {
        left: 15px;
    }

    .experience-item::after {
        left: 7px !important;
    }

    .experience-card {
        padding: 1.2rem;
    }

    .project-description {
        font-size: 0.85rem;
    }

    .tech-tag {
        font-size: 0.7rem;
        padding: 0.25rem 0.5rem;
    }
}

/* Améliorer les performances des animations */
.experience-card,
.tech-tag,
.achievement {
    will-change: transform;
}
</style>