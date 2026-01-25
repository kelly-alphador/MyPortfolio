<template>
  <section class="about" id="about">
    <div class="about-container">
      <h2 class="about-title">a propos</h2>
      <p class="about-intro">
        Passionné par le développement et l'innovation, je transforme des
        concepts en solutions digitales performantes avec une approche centrée
        sur l'utilisateur et la qualité.
      </p>

      <div class="about-description">
        <p>
          Développeur <strong>Full-Stack .NET & Vue.js</strong>, je conçois des solutions web et desktop 
          sur mesure. Mon expertise s'étend de la création d'architectures robustes avec 
          <strong>ASP.NET Core Web API</strong> et <strong>MVC</strong>, au développement d'applications 
          Windows via <strong>WPF</strong>. Côté front-end, j'exploite la puissance de 
          <strong>Vue.js</strong> pour bâtir des interfaces modernes, réactives et centrées sur l'expérience utilisateur.
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
