<template>
  <section class="experience" id="experience">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Expériences</h2>
      </div>
      
      <div class="experience-grid">

        <!-- Spray Info Experience (MOST RECENT) -->
        <div class="experience-card">
          <div class="experience-header">
            <div class="company-info">
              <h3 class="company-name">SPRAY INFO</h3>
              <span class="experience-duration">Août 2024 - Décembre 2024</span>
            </div>
            <h4 class="job-title">Développeur .NET (Stagiaire)</h4>
          </div>
          
          <div class="experience-content">
            <h5 class="project-title">Plateforme E-commerce B2B – TAMAOIL</h5>
            <p class="project-description">
              Développement d'une plateforme de vente en ligne permettant aux clients d’acheter des produits 
              et aux administrateurs de gérer les ventes, les stocks et les commandes. 
              L’application inclut un système d’alertes pour les ruptures de stock, 
              la gestion des avis clients et le paiement en ligne via PayPal.
            </p>
            
            <div class="tech-stack">
              <span class="tech-tag">ASP.NET MVC</span>
              <span class="tech-tag">.NET Framework</span>
              <span class="tech-tag">C#</span>
              <span class="tech-tag">SQL Server</span>
              <span class="tech-tag">JavaScript</span>
              <span class="tech-tag">jQuery</span>
              <span class="tech-tag">Bootstrap</span>
            </div>
            
            <ul class="achievements">
              <li class="achievement-item">
                <div class="achievement-dot"></div>
                <span>Développement complet du système de gestion des commandes</span>
              </li>
              <li class="achievement-item">
                <div class="achievement-dot"></div>
                <span>Mise en place des paiements en ligne via PayPal</span>
              </li>
              <li class="achievement-item">
                <div class="achievement-dot"></div>
                <span>Système d’alerte pour les produits en rupture de stock</span>
              </li>
              <li class="achievement-item">
                <div class="achievement-dot"></div>
                <span>Gestion des avis et commentaires clients</span>
              </li>
            </ul>
          </div>
        </div>


        <!-- WBS Experience -->
        <div class="experience-card">
          <div class="experience-header">
            <div class="company-info">
              <h3 class="company-name">WBS – World Business Solution</h3>
              <span class="experience-duration">Septembre 2023 - Décembre 2023</span>
            </div>
            <h4 class="job-title">Développeur Full-Stack (Stagiaire)</h4>
          </div>
          
          <div class="experience-content">
            <h5 class="project-title">Application de Gestion de Devis – Entreprise AINA (Tuléar)</h5>
            <p class="project-description">
              Conception et développement d’une application web permettant la gestion complète des devis clients. 
              La solution permet de gérer les sites des clients, les unités matérielles, les équipements, 
              les devis et la génération automatique des devis en format PDF.
            </p>
            
            <div class="tech-stack">
              <span class="tech-tag">Symfony</span>
              <span class="tech-tag">Vue.js</span>
              <span class="tech-tag">PHP</span>
              <span class="tech-tag">MySQL</span>
              <span class="tech-tag">JavaScript</span>
            </div>
            
            <ul class="achievements">
              <li class="achievement-item">
                <div class="achievement-dot"></div>
                <span>Automatisation de la génération des devis en PDF</span>
              </li>
              <li class="achievement-item">
                <div class="achievement-dot"></div>
                <span>Gestion des clients, matériels et unités techniques</span>
              </li>
              <li class="achievement-item">
                <div class="achievement-dot"></div>
                <span>Interface moderne et responsive</span>
              </li>
            </ul>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>


<script>
export default {
  name: 'Experience',
  mounted() {
    // Observer pour les animations d'apparition
    this.initAnimations();
  },
  methods: {
    initAnimations() {
      const observerOptions = {
        root: null,
        rootMargin: '0px',
        threshold: 0.1
      };

      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('animated');
          }
        });
      }, observerOptions);

      // Observer chaque carte d'expérience
      document.querySelectorAll('.experience-card').forEach(card => {
        observer.observe(card);
      });
    }
  }
}
</script>

<style scoped>
/* Import de la police Syncopate */
@import url('https://fonts.googleapis.com/css2?family=Syncopate:wght@400;500;700&display=swap');

/* Variables */
.experience {
    --emerald-primary: #50C878;
    --emerald-dark: #2E8B57;
    --emerald-light: #A8E6CF;
    --text-primary: #FFFFFF;
    --text-secondary: #E8F5E9;
    --text-muted: #C4E0A4;
    padding: 100px 20px;
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
    font-family: 'Syncopate', sans-serif;
    font-weight: 600;
    font-size: clamp(2.5rem, 5vw, 3.5rem);
    color: var(--emerald-primary);
    letter-spacing: 3px;
    position: relative;
    padding-bottom: 15px;
}

.section-title::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 80px;
    height: 2px;
    background: var(--emerald-primary);
}

/* Grid pour les cartes */
.experience-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
    gap: 3rem;
    max-width: 1000px;
    margin: 0 auto;
}

/* Carte d'expérience */
.experience-card {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.6s ease, transform 0.6s ease;
}

.experience-card.animated {
    opacity: 1;
    transform: translateY(0);
}

/* En-tête de l'expérience */
.experience-header {
    margin-bottom: 1.5rem;
    border-bottom: 1px solid rgba(80, 200, 120, 0.2);
    padding-bottom: 1rem;
}

.company-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 0.5rem;
}

.company-name {
    font-family: 'Syncopate', sans-serif;
    font-weight: 500;
    font-size: 1.2rem;
    color: var(--emerald-primary);
    letter-spacing: 1px;
    text-transform: uppercase;
}

.experience-duration {
    color: var(--text-muted);
    font-size: 0.85rem;
    background: rgba(80, 200, 120, 0.1);
    padding: 0.3rem 0.8rem;
    border-radius: 12px;
    font-weight: 500;
}

.job-title {
    color: var(--text-primary);
    font-size: 1.1rem;
    font-weight: 600;
}

/* Contenu de l'expérience */
.experience-content {
    padding-top: 0.5rem;
}

.project-title {
    color: var(--emerald-light);
    font-size: 1.1rem;
    font-weight: 600;
    margin-bottom: 1rem;
}

.project-description {
    color: var(--text-secondary);
    line-height: 1.6;
    margin-bottom: 1.5rem;
    font-size: 1rem;
}

/* Stack technique - Style shadcn */
.tech-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    margin-bottom: 1.5rem;
}

.tech-tag {
    background: rgba(80, 200, 120, 0.08);
    color: var(--emerald-light);
    padding: 0.2rem 0.6rem;
    border-radius: 6px;
    font-size: 0.75rem;
    font-weight: 500;
    border: 1px solid rgba(80, 200, 120, 0.2);
    transition: all 0.2s ease;
    height: 24px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    line-height: 1;
}

.tech-tag:hover {
    background: rgba(80, 200, 120, 0.15);
    border-color: rgba(80, 200, 120, 0.3);
}

/* Réalisations avec puces */
.achievements {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: 0.6rem;
}

.achievement-item {
    display: flex;
    align-items: flex-start;
    color: var(--text-muted);
    font-size: 0.9rem;
    line-height: 1.4;
}

.achievement-dot {
    width: 6px;
    height: 6px;
    background: var(--emerald-primary);
    border-radius: 50%;
    margin-right: 0.8rem;
    margin-top: 0.5rem;
    flex-shrink: 0;
}

.achievement-item span {
    flex: 1;
}

/* Animation décalée pour chaque carte */
.experience-card:nth-child(1).animated {
    animation: fadeInUp 0.6s ease 0.1s forwards;
}

.experience-card:nth-child(2).animated {
    animation: fadeInUp 0.6s ease 0.3s forwards;
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* RESPONSIVE DESIGN */
@media (max-width: 1100px) {
    .experience-grid {
        grid-template-columns: 1fr;
        max-width: 700px;
    }
}

@media (max-width: 768px) {
    .experience {
        padding: 80px 15px;
    }

    .section-header {
        margin-bottom: 3rem;
    }

    .section-title {
        font-size: clamp(2rem, 4vw, 2.5rem);
        letter-spacing: 2px;
    }

    .experience-grid {
        gap: 2rem;
    }

    .company-info {
        flex-direction: column;
        align-items: flex-start;
        gap: 0.5rem;
    }

    .company-name {
        font-size: 1.1rem;
    }

    .experience-duration {
        font-size: 0.8rem;
        padding: 0.2rem 0.6rem;
    }

    .job-title {
        font-size: 1rem;
    }

    .project-title {
        font-size: 1rem;
        margin-bottom: 0.8rem;
    }

    .project-description {
        font-size: 0.9rem;
        margin-bottom: 1.2rem;
    }

    .tech-stack {
        gap: 0.3rem;
        margin-bottom: 1.2rem;
    }

    .tech-tag {
        font-size: 0.7rem;
        padding: 0.2rem 0.5rem;
        height: 22px;
    }

    .achievements {
        gap: 0.5rem;
    }

    .achievement-item {
        font-size: 0.85rem;
    }

    .achievement-dot {
        margin-top: 0.4rem;
    }
}

@media (max-width: 480px) {
    .experience {
        padding: 60px 10px;
    }

    .section-title {
        font-size: 1.8rem;
        letter-spacing: 1px;
    }

    .experience-grid {
        gap: 1.5rem;
    }

    .experience-card {
        padding: 0;
    }

    .project-description {
        font-size: 0.85rem;
    }

    .tech-tag {
        font-size: 0.65rem;
        padding: 0.15rem 0.4rem;
        height: 20px;
    }

    .achievement-item {
        font-size: 0.8rem;
    }
}
</style>