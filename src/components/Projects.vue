<template>
  <section class="projects" id="projects">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">projets</h2>
      </div>

      <div class="projects-grid">
        <!-- Boucle dynamique sur les projets -->
        <div 
          v-for="(project, index) in projects" 
          :key="index"
          class="project-card"
        >
          <div class="project-image">
            <img 
              :src="project.image" 
              :alt="project.imageAlt" 
              class="project-img"
            >
            <div class="project-links">
              <a :href="project.demoLink" class="demo-link" target="_blank">
                <svg class="link-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                        d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                        d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"/>
                </svg>
                Démo
              </a>
              <a :href="project.githubLink" class="github-link" target="_blank">
                <svg class="link-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                        d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
                </svg>
                Code
              </a>
            </div>
          </div>

          <div class="project-header">
            <h3 class="project-title">{{ project.title }}</h3>
            <span class="project-category">{{ project.category }}</span>
          </div>

          <div class="project-content">
            <p class="project-description">
              {{ project.description }}
            </p>

            <div class="project-tech">
              <span 
                v-for="(tech, techIndex) in project.technologies" 
                :key="techIndex"
                class="tech-badge"
              >
                {{ tech }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import shopMasterImg from '@/assets/images/image_app/shopMaster1.png'
import chronoDevImg from '@/assets/images/image_app/chronodev.png'
import portfolioImg from '@/assets/images/image_app/portfolio.png'
import dantzigImg from '@/assets/images/image_app/DANDZIG.png'
import taskManagerImg from '@/assets/images/image_app/Gestion_tacche.png'
export default {
  name: "Projects",
  data() {
    return {
        projects: [
  {
    title: "ShopMaster",
    category: "Application Web E-commerce",
    description: `ShopMaster est une application e-commerce conçue pour répondre aux difficultés rencontrées par les commerces traditionnels. Avant sa mise en place, les clients devaient se déplacer pour effectuer leurs achats, ce qui entraînait une perte de temps. De plus, la gestion des ventes se faisait manuellement via Excel, rendant le suivi du stock peu fiable. Les ruptures de stock n'étaient pas toujours détectées à temps, ce qui provoquait des frustrations lorsque les clients cherchaient des produits indisponibles.

L'application permet désormais aux clients d'acheter des produits en ligne facilement, tandis que les administrateurs disposent d'un système centralisé pour gérer les produits, les ventes, les commandes et le stock en temps réel. ShopMaster inclut un paiement sécurisé via PayPal, la création de comptes clients, une confirmation par email après achat et l'envoi automatique de factures. Cette solution améliore l'expérience client, réduit les pertes liées aux erreurs de gestion et optimise le suivi des ventes.`
,
    image: shopMasterImg,
    imageAlt: "Capture d'écran ShopMaster",
    demoLink: "#",
    githubLink: "#",
    technologies: ["ASP.NET Core MVC", "C#", "JavaScript", "Bootstrap", "SQL Server"]
  },
  {
    title: "ChronoDev",
    category: "Application Web de Gestion de Projets",
    description: `ChronoDev est une application de gestion des feuilles de temps conçue pour les entreprises informatiques. Avant sa mise en place, le suivi des heures de travail se faisait de manière informelle ou via des fichiers Excel, ce qui rendait difficile le contrôle du temps réellement passé sur chaque projet. Les managers manquaient de visibilité sur la productivité des équipes, et les développeurs n’avaient pas toujours de retour clair sur la validation de leurs heures.

L’application introduit un système structuré avec trois rôles : Manager, Chef de projet et Développeur. Les développeurs et chefs de projet saisissent leurs heures de travail par projet et par jour. Le manager peut consulter ces saisies, puis les valider ou les refuser avec un commentaire expliquant la raison du refus.

Chaque utilisateur peut suivre l’état de ses déclarations : les heures validées apparaissent en vert, celles refusées en rouge, avec accès au détail du motif de refus. L’application permet également de visualiser le temps restant alloué à un projet, offrant ainsi une meilleure anticipation des délais et une gestion plus efficace des ressources.

ChronoDev améliore la transparence, facilite le suivi de la productivité et aide les entreprises à mieux contrôler l’avancement réel de leurs projets.`,
  
    image: chronoDevImg,
    imageAlt: "Capture d'écran ChronoDev",
    demoLink: "#",
    githubLink: "#",
    technologies: ["Vue.js", "Nuxt.js", ".NET Core Web API", "SQL Server"]
  },
  {
    title: "Portfolio Interactif",
    category: "Portfolio Web",
     description: `Ce portfolio interactif a été conçu pour répondre à un besoin essentiel : présenter clairement mes compétences et mes projets dans un format professionnel, moderne et accessible à tous. Avant sa création, mes réalisations étaient dispersées entre différents supports, ce qui rendait difficile pour un recruteur ou un client d’avoir une vision globale de mon profil et de mon savoir-faire.

L’objectif de cette plateforme est de centraliser mes projets, démontrer mes compétences techniques à travers des cas concrets et offrir une navigation fluide et agréable. Le site met en avant des projets réels, chacun présenté avec le problème rencontré, la solution développée et les technologies utilisées.

Grâce à une interface responsive, des animations modernes et un design soigné, ce portfolio reflète à la fois mes compétences en développement front-end et mon attention à l’expérience utilisateur. Il constitue un outil professionnel qui facilite la mise en relation avec des recruteurs, des entreprises et des clients potentiels.`,
    image: portfolioImg,
    imageAlt: "Capture d'écran Portfolio",
    demoLink: "#",
    githubLink: "#",
    technologies: ["Vue.js", "JavaScript", "CSS3"]
  },
  {
    title: "Algorithme de Dantzig",
    category: "Application Desktop",
    description: `Cette application desktop a été développée pour faciliter l’apprentissage des algorithmes de graphes, notamment l’algorithme de Dantzig utilisé pour déterminer les chemins minimaux et maximaux. Avant sa mise en place, les étudiants devaient effectuer ces calculs manuellement, ce qui demandait beaucoup de temps et augmentait le risque d’erreurs, surtout pour les graphes complexes.

L’application permet de modéliser un graphe à travers une interface graphique intuitive, avec visualisation des sommets et des arcs. L’utilisateur peut ensuite lancer automatiquement le calcul des chemins minimaux et maximaux, obtenant des résultats rapides et fiables.

Cette solution aide les étudiants à mieux comprendre le fonctionnement de l’algorithme grâce à la visualisation, tout en réduisant le temps consacré aux calculs manuels. Elle constitue ainsi un outil pédagogique interactif qui rend l’apprentissage plus efficace et plus clair.`,
    image: dantzigImg,
    imageAlt: "Capture d'écran Algorithme de Dantzig",
    demoLink: "#",
    githubLink: "#",
    technologies: ["C#", "WPF", ".NET"]
  },
  {
    title: "Gestion de Tâches",
    category: "Application Desktop",
    description: "Application de gestion de tâches permettant d’ajouter, modifier, supprimer et suivre l’état des tâches. Interface simple et efficace pour améliorer l’organisation du travail.",
    image: taskManagerImg,
    imageAlt: "Capture d'écran Gestion de Tâches",
    demoLink: "#",
    githubLink: "#",
    technologies: ["C#", "Windows Forms", ".NET"]
  }
]

    };
  },
  mounted() {
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

      document.querySelectorAll(".project-card").forEach((card) => {
        observer.observe(card);
      });
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Syncopate:wght@400;500;700&display=swap");

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
  gap: 2.5rem;
  max-width: 1100px;
  margin: 0 auto;
}

/* Carte de projet */
.project-card {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.4s ease;
  border: 1px solid rgba(80, 200, 120, 0.1);
  border-radius: 16px;
  padding: 0;
  overflow: hidden;
  background: rgba(20, 30, 25, 0.3);
  backdrop-filter: blur(10px);
}

.project-card.animated {
  opacity: 1;
  transform: translateY(0);
}

.project-card:hover {
  border-color: rgba(80, 200, 120, 0.3);
  transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(80, 200, 120, 0.15);
}

/* Section image - Ajustée pour remplir le cadre */
.project-image {
  position: relative;
  height: 280px;
  overflow: hidden;
  border-bottom: 1px solid rgba(80, 200, 120, 0.1);
  background: linear-gradient(135deg, #15231c 0%, #1e3429 100%);
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center top;
  background: rgba(30, 40, 35, 0.5);
  transition: transform 0.5s ease;
}

/* Pour les images de placeholder */
.project-img[src*="placeholder"] {
  object-fit: contain;
  padding: 20px;
  background: linear-gradient(135deg, #1a2f27 0%, #2e8b57 100%);
}

/* Effet de zoom au survol */
.project-card:hover .project-img {
  transform: scale(1.05);
}

/* Liens sur l'image */
.project-links {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(20, 30, 25, 0.92);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  opacity: 0;
  transition: opacity 0.3s ease;
  z-index: 2;
}

.project-image:hover .project-links {
  opacity: 1;
}

.demo-link, .github-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem 1.5rem;
  border-radius: 8px;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.3s ease;
  font-size: 0.9rem;
}

.demo-link {
  background: var(--emerald-primary);
  color: white;
  border: 2px solid var(--emerald-primary);
}

.github-link {
  background: transparent;
  color: var(--emerald-primary);
  border: 2px solid var(--emerald-primary);
}

.demo-link:hover {
  background: var(--emerald-dark);
  border-color: var(--emerald-dark);
  transform: translateY(-2px);
}

.github-link:hover {
  background: rgba(80, 200, 120, 0.1);
  transform: translateY(-2px);
}

.link-icon {
  width: 18px;
  height: 18px;
  stroke-width: 2;
}

/* Contenu de la carte */
.project-header {
  padding: 1.5rem 1.5rem 0.5rem;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.project-title {
  color: var(--text-primary);
  font-size: 1.3rem;
  font-weight: 600;
  margin: 0;
}

.project-category {
  color: var(--emerald-primary);
  font-size: 0.8rem;
  font-weight: 500;
  background: rgba(80, 200, 120, 0.1);
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.project-content {
  padding: 0 1.5rem 1.5rem;
}

.project-description {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.5rem;
  font-size: 0.95rem;
}

/* Technologies */
.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tech-badge {
  background: rgba(80, 200, 120, 0.08);
  color: var(--emerald-light);
  padding: 0.3rem 0.8rem;
  border-radius: 6px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid rgba(80, 200, 120, 0.2);
  transition: all 0.2s ease;
  height: 28px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  line-height: 1;
}

.tech-badge:hover {
  background: rgba(80, 200, 120, 0.15);
  border-color: rgba(80, 200, 120, 0.3);
  transform: translateY(-1px);
}

/* Suppression des statistiques */
.project-stats {
  display: none;
}

/* Animations décalées */
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
    gap: 2rem;
  }

  .project-image {
    height: 240px;
  }

  .project-img {
    object-position: center;
  }

  .project-links {
    gap: 1rem;
  }

  .demo-link, .github-link {
    padding: 0.6rem 1.2rem;
    font-size: 0.85rem;
  }

  .link-icon {
    width: 16px;
    height: 16px;
  }

  .project-header {
    padding: 1.25rem 1.25rem 0.5rem;
  }

  .project-title {
    font-size: 1.2rem;
  }

  .project-content {
    padding: 0 1.25rem 1.25rem;
  }

  .project-description {
    font-size: 0.9rem;
  }

  .tech-badge {
    font-size: 0.75rem;
    padding: 0.25rem 0.6rem;
    height: 26px;
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

  .project-image {
    height: 220px;
  }

  .project-img[alt*="Portfolio"] {
    object-position: center 20%;
  }

  .project-links {
    flex-direction: column;
    gap: 0.8rem;
  }

  .project-header {
    flex-direction: column;
    gap: 0.5rem;
    align-items: flex-start;
  }

  .project-category {
    align-self: flex-start;
  }
}
</style>