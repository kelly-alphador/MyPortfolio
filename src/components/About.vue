<template>
  <section class="about" id="about">
    <div class="about-container">
      <h2 class="about-title">a propos</h2>
      <p class="about-intro">
          Passionné par le développement logiciel et l'innovation, je transforme des problématiques réelles en solutions digitales performantes, avec une approche centrée sur l'utilisateur, l'efficacité et la qualité.
      </p>

      <div class="about-description">
        <p>
            Actuellement étudiant en Master 2 à l'École Nationale d'Informatique (ENI), je développe des applications web en utilisant différentes technologies, notamment PHP (Symfony),Node.js, ASP.NET, Vue.js et Angular. J'accompagne les entreprises et les porteurs de projets dans la conception de solutions permettant d'optimiser les processus métier et d'améliorer la gestion de leurs activités.
        </p>
        <p>
          J'accorde une importance particulière à la conception d'applications robustes, à l'utilisation d'API REST, à la modélisation des bases de données et à l'application des bonnes pratiques de développement telles que la Clean Architecture, le DDD et les tests. J'apprécie également travailler avec Git, Docker et les outils modernes qui facilitent la qualité et la collaboration.
        </p>
        <p>
          Curieux, rigoureux et doté d'une forte capacité d'apprentissage, je m'adapte rapidement aux nouvelles technologies. Mon objectif est de concevoir des solutions fiables, maintenables et utiles, qui apportent une réelle valeur aux utilisateurs et aux organisations.
        </p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "About",
};
</script>

<style scoped>
/* Import de la police Syncopate */
@import url("https://fonts.googleapis.com/css2?family=Syncopate:wght@400;500;700&display=swap");

/* Variables */
.about {
  --emerald-primary: #50c878;
  --text-primary: #ffffff;
  --text-muted: #c4e0a4;
}

/* Section About */
.about {
  padding: 100px 20px;
  text-align: justify;
}

.about-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;;
  gap: 40px;
}

/* Titre */
.about-title {
  font-family: "Syncopate", sans-serif;
  font-weight: 600;
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  color: var(--emerald-primary);
  letter-spacing: 3px;
  /* text-transform: uppercase; */
  position: relative;
  padding-bottom: 15px;
}

.about-title::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 2px;
  background: var(--emerald-primary);
}

/* Texte d'introduction */
.about-intro {
  font-size: clamp(1.2rem, 3vw, 1.5rem);
  color: var(--text-primary);
  line-height: 1.6;
  max-width: 900px;
  font-weight: 300;
}

/* Description - sans fond ni bordure */
.about-description {
  max-width: 900px;
  margin: 0 auto;
}

.about-description p {
  font-size: clamp(1rem, 2.5vw, 1.2rem);
  color: var(--text-muted);
  line-height: 1.8;
  /* text-align: center; */
  margin: 0;
}

/* Animation d'apparition */
.about {
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 1s ease-out forwards;
}

.about-title {
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.3s forwards;
}

.about-intro {
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.5s forwards;
}

.about-description {
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.7s forwards;
}

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

/* Responsive */
@media (max-width: 968px) {
  .about {
    padding: 80px 15px;
  }

  .about-container {
    gap: 30px;
  }
}

@media (max-width: 768px) {
  .about {
    padding: 60px 10px;
  }

  .about-title {
    font-size: clamp(2rem, 4vw, 2.5rem);
    letter-spacing: 2px;
  }

  .about-intro {
    font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  }

  .about-description p {
    font-size: clamp(0.95rem, 2vw, 1.1rem);
    line-height: 1.7;
  }
}

@media (max-width: 480px) {
  .about {
    padding: 50px 10px;
  }

  .about-title {
    font-size: 1.8rem;
    letter-spacing: 1px;
  }

  .about-intro {
    font-size: 1rem;
  }

  .about-description p {
    font-size: 0.9rem;
    line-height: 1.6;
  }
}
</style>