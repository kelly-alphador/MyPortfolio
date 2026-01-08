<template>
  <section class="projects" id="projects">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">mes projets</h2>
      </div>

      <div class="projects-grid">
        <!-- Project 1: WBS Quote Management -->
        <div class="project-card">
          <div class="project-header">
            <h3 class="project-title">Gestion de Devis WBS</h3>
            <span class="project-category">Application Web</span>
          </div>

          <div class="project-content">
            <p class="project-description">
              Application full-stack moderne pour la gestion automatisée des
              devis avec interface Vue.js et backend Symfony robuste.
            </p>

            <div class="project-tech">
              <span class="tech-badge">Symfony</span>
              <span class="tech-badge">Vue.js</span>
              <span class="tech-badge">MySQL</span>
              <span class="tech-badge">JavaScript</span>
            </div>

            <div class="project-stats">
              <div class="stat">
                <span class="stat-number">40%</span>
                <span class="stat-label">Gain d'efficacité</span>
              </div>
              <div class="stat">
                <span class="stat-number">100+</span>
                <span class="stat-label">Devis/jour</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Project 2: Spray Info E-commerce -->
        <div class="project-card">
          <div class="project-header">
            <h3 class="project-title">Spray Info B2B</h3>
            <span class="project-category">E-commerce</span>
          </div>

          <div class="project-content">
            <p class="project-description">
              Plateforme e-commerce B2B complète avec gestion avancée des
              stocks, système de paiement et dashboard administrateur.
            </p>

            <div class="project-tech">
              <span class="tech-badge">ASP.NET MVC</span>
              <span class="tech-badge">C#</span>
              <span class="tech-badge">SQL Server</span>
              <span class="tech-badge">Entity Framework</span>
            </div>

            <div class="project-stats">
              <div class="stat">
                <span class="stat-number">500+</span>
                <span class="stat-label">Produits</span>
              </div>
              <div class="stat">
                <span class="stat-number">24/7</span>
                <span class="stat-label">Disponibilité</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Project 3: Portfolio Showcase -->
        <div class="project-card">
          <div class="project-header">
            <h3 class="project-title">Portfolio Interactif</h3>
            <span class="project-category">Portfolio</span>
          </div>

          <div class="project-content">
            <p class="project-description">
              Portfolio personnel moderne avec animations avancées, design
              responsive et architecture .NET Core pour les projets futurs.
            </p>

            <div class="project-tech">
              <span class="tech-badge">.NET Core</span>
              <span class="tech-badge">Vue.js</span>
              <span class="tech-badge">CSS3</span>
              <span class="tech-badge">JavaScript</span>
            </div>

            <div class="project-stats">
              <div class="stat">
                <span class="stat-number">100%</span>
                <span class="stat-label">Responsive</span>
              </div>
              <div class="stat">
                <span class="stat-number">A+</span>
                <span class="stat-label">Performance</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Projects",
  mounted() {
    // Observer pour les animations d'apparition
    this.initAnimations();
  },
  methods: {
    initAnimations() {
      const observerOptions = {
        root: null,
        rootMargin: "0px",
        threshold: 0.1,
      };

      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add("animated");
          }
        });
      }, observerOptions);

      // Observer chaque carte de projet
      document.querySelectorAll(".project-card").forEach((card) => {
        observer.observe(card);
      });
    },
  },
};
</script>

<style scoped>
/* Import de la police Syncopate */
@import url("https://fonts.googleapis.com/css2?family=Syncopate:wght@400;500;700&display=swap");

/* Variables */
.projects {
  --emerald-primary: #50c878;
  --emerald-dark: #2e8b57;
  --emerald-light: #a8e6cf;
  --text-primary: #ffffff;
  --text-secondary: #e8f5e9;
  --text-muted: #c4e0a4;
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
  font-family: "Syncopate", sans-serif;
  font-weight: 600;
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  color: var(--emerald-primary);
  letter-spacing: 3px;
  position: relative;
  padding-bottom: 15px;
}

.section-title::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 2px;
  background: var(--emerald-primary);
}

/* Grid pour les cartes */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  max-width: 1100px;
  margin: 0 auto;
}

/* Carte de projet simplifiée */
.project-card {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
  border: 1px solid rgba(80, 200, 120, 0.1);
  border-radius: 12px;
  padding: 1.5rem;
}

.project-card.animated {
  opacity: 1;
  transform: translateY(0);
}

.project-card:hover {
  border-color: rgba(80, 200, 120, 0.3);
  transform: translateY(-5px);
}

/* En-tête du projet */
.project-header {
  margin-bottom: 1.5rem;
  border-bottom: 1px solid rgba(80, 200, 120, 0.2);
  padding-bottom: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.project-title {
  color: var(--text-primary);
  font-size: 1.2rem;
  font-weight: 600;
  margin: 0;
}

.project-category {
  color: var(--emerald-primary);
  font-size: 0.8rem;
  font-weight: 500;
  background: rgba(80, 200, 120, 0.1);
  padding: 0.2rem 0.6rem;
  border-radius: 12px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Contenu du projet */
.project-content {
  padding-top: 0.5rem;
}

.project-description {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.5rem;
  font-size: 0.95rem;
}

/* Technologies - Badges shadcn style */
.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  margin-bottom: 1.5rem;
}

.tech-badge {
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

.tech-badge:hover {
  background: rgba(80, 200, 120, 0.15);
  border-color: rgba(80, 200, 120, 0.3);
}

/* Statistiques */
.project-stats {
  display: flex;
  gap: 1.5rem;
  padding-top: 1rem;
  border-top: 1px solid rgba(80, 200, 120, 0.1);
}

.stat {
  text-align: center;
  flex: 1;
}

.stat-number {
  display: block;
  color: var(--emerald-primary);
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 0.2rem;
}

.stat-label {
  color: var(--text-muted);
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Animations décalées pour chaque carte */
.project-card:nth-child(1).animated {
  animation: fadeInUp 0.6s ease 0.1s forwards;
}

.project-card:nth-child(2).animated {
  animation: fadeInUp 0.6s ease 0.2s forwards;
}

.project-card:nth-child(3).animated {
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
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
    max-width: 800px;
  }
}

@media (max-width: 768px) {
  .projects {
    padding: 80px 15px;
  }

  .section-header {
    margin-bottom: 3rem;
  }

  .section-title {
    font-size: clamp(2rem, 4vw, 2.5rem);
    letter-spacing: 2px;
  }

  .projects-grid {
    grid-template-columns: 1fr;
    max-width: 500px;
    gap: 1.5rem;
  }

  .project-card {
    padding: 1.25rem;
  }

  .project-header {
    margin-bottom: 1.25rem;
    padding-bottom: 0.75rem;
  }

  .project-title {
    font-size: 1.1rem;
  }

  .project-category {
    font-size: 0.75rem;
    padding: 0.15rem 0.5rem;
  }

  .project-description {
    font-size: 0.9rem;
    margin-bottom: 1.25rem;
  }

  .project-tech {
    gap: 0.3rem;
    margin-bottom: 1.25rem;
  }

  .tech-badge {
    font-size: 0.7rem;
    padding: 0.2rem 0.5rem;
    height: 22px;
  }

  .project-stats {
    gap: 1rem;
  }

  .stat-number {
    font-size: 1rem;
  }

  .stat-label {
    font-size: 0.7rem;
  }
}

@media (max-width: 480px) {
  .projects {
    padding: 60px 10px;
  }

  .section-title {
    font-size: 1.8rem;
    letter-spacing: 1px;
  }

  .projects-grid {
    gap: 1.25rem;
  }

  .project-card {
    padding: 1rem;
  }

  .project-title {
    font-size: 1rem;
  }

  .project-description {
    font-size: 0.85rem;
  }

  .tech-badge {
    font-size: 0.65rem;
    padding: 0.15rem 0.4rem;
    height: 20px;
  }

  .stat-number {
    font-size: 0.9rem;
  }

  .stat-label {
    font-size: 0.65rem;
  }
}
</style>
