<template>
  <section class="skills" id="skills">
    <div class="container">
      <div class="section-header" data-aos="fade-up" data-aos-duration="1000">
        <h2 class="section-title">mes compétences</h2>
      </div>
      <div class="scroll-wrapper">
        <div id="icons-list">
          <!-- HTML -->
          <div class="techno-container">
            <img
              src="@/assets/images/html.svg"
              alt="HTML"
              class="techno-icon"
            />
            <span>HTML</span>
          </div>
          <!-- CSS -->
          <div class="techno-container">
            <img src="@/assets/images/css.svg" alt="CSS" class="techno-icon" />
            <span>CSS</span>
          </div>
          <!-- JavaScript -->
          <div class="techno-container">
            <img
              src="@/assets/images/javascript.svg"
              alt="JavaScript"
              class="techno-icon"
            />
            <span>JavaScript</span>
          </div>
          <!-- C# -->
          <div class="techno-container">
            <img
              src="@/assets/images/csharp.svg"
              alt="C#"
              class="techno-icon"
            />
            <span>C#</span>
          </div>
          <!-- .NET -->
          <div class="techno-container">
            <img
              src="@/assets/images/dotnet.svg"
              alt=".NET"
              class="techno-icon"
            />
            <span>.NET</span>
          </div>
          <!-- Vue.js -->
          <div class="techno-container">
            <img
              src="@/assets/images/vue.svg"
              alt="Vue.js"
              class="techno-icon"
            />
            <span>Vue.js</span>
          </div>
          <!-- MySQL -->
          <div class="techno-container">
            <img
              src="@/assets/images/mysql.svg"
              alt="MySQL"
              class="techno-icon"
            />
            <span>MySQL</span>
          </div>
          <!-- Docker -->
          <div class="techno-container">
            <img
              src="@/assets/images/docker.svg"
              alt="Docker"
              class="techno-icon"
            />
            <span>Docker</span>
          </div>
          <!-- Git -->
          <div class="techno-container">
            <img src="@/assets/images/git.svg" alt="Git" class="techno-icon" />
            <span>Git</span>
          </div>
          <!-- Bootstrap -->
          <div class="techno-container">
            <img
              src="@/assets/images/bootstrap.svg"
              alt="Bootstrap"
              class="techno-icon"
            />
            <span>Bootstrap</span>
          </div>
          <!-- Tailwind -->
          <div class="techno-container">
            <img
              src="@/assets/images/tailwind.svg"
              alt="Tailwind CSS"
              class="techno-icon"
            />
            <span>Tailwind</span>
          </div>
          <!-- jQuery -->
          <div class="techno-container">
            <img
              src="@/assets/images/jquery.svg"
              alt="jQuery"
              class="techno-icon"
            />
            <span>jQuery</span>
          </div>
          <!-- Duplication pour effet infini -->
          <!-- HTML -->
          <div class="techno-container">
            <img
              src="@/assets/images/html.svg"
              alt="HTML"
              class="techno-icon"
            />
            <span>HTML</span>
          </div>
          <!-- CSS -->
          <div class="techno-container">
            <img src="@/assets/images/css.svg" alt="CSS" class="techno-icon" />
            <span>CSS</span>
          </div>
          <!-- JavaScript -->
          <div class="techno-container">
            <img
              src="@/assets/images/javascript.svg"
              alt="JavaScript"
              class="techno-icon"
            />
            <span>JavaScript</span>
          </div>
          <!-- C# -->
          <div class="techno-container">
            <img
              src="@/assets/images/csharp.svg"
              alt="C#"
              class="techno-icon"
            />
            <span>C#</span>
          </div>
          <!-- .NET -->
          <div class="techno-container">
            <img
              src="@/assets/images/dotnet.svg"
              alt=".NET"
              class="techno-icon"
            />
            <span>.NET</span>
          </div>
          <!-- Vue.js -->
          <div class="techno-container">
            <img
              src="@/assets/images/vue.svg"
              alt="Vue.js"
              class="techno-icon"
            />
            <span>Vue.js</span>
          </div>
          <!-- MySQL -->
          <div class="techno-container">
            <img
              src="@/assets/images/mysql.svg"
              alt="MySQL"
              class="techno-icon"
            />
            <span>MySQL</span>
          </div>
          <!-- Docker -->
          <div class="techno-container">
            <img
              src="@/assets/images/docker.svg"
              alt="Docker"
              class="techno-icon"
            />
            <span>Docker</span>
          </div>
          <!-- Git -->
          <div class="techno-container">
            <img src="@/assets/images/git.svg" alt="Git" class="techno-icon" />
            <span>Git</span>
          </div>
          <!-- Bootstrap -->
          <div class="techno-container">
            <img
              src="@/assets/images/bootstrap.svg"
              alt="Bootstrap"
              class="techno-icon"
            />
            <span>Bootstrap</span>
          </div>
          <!-- Tailwind -->
          <div class="techno-container">
            <img
              src="@/assets/images/tailwind.svg"
              alt="Tailwind CSS"
              class="techno-icon"
            />
            <span>Tailwind</span>
          </div>
          <!-- jQuery -->
          <div class="techno-container">
            <img
              src="@/assets/images/jquery.svg"
              alt="jQuery"
              class="techno-icon"
            />
            <span>jQuery</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// Pas besoin d'imports supplémentaires
</script>

<style scoped>
/* Import de la police Syncopate */
@import url("https://fonts.googleapis.com/css2?family=Syncopate:wght@400;500;700&display=swap");

/* Variables */
.skills {
  --emerald-primary: #50c878;
  --emerald-dark: #2e8b57;
  --text-primary: #ffffff;
  --text-secondary: #e8f5e9;
  position: relative;
  padding: 100px 20px;
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

.scroll-wrapper {
  overflow: hidden;
  width: 100%;
  margin-top: 100px;
  padding: 20px;
}

#icons-list {
  display: flex;
  gap: 60px;
  animation: scroll-left 30s linear infinite;
  width: fit-content;
}

#icons-list:hover {
  animation-play-state: paused;
}

@keyframes scroll-left {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.techno-container {
  text-align: center;
  color: var(--text-secondary);
  transition: all 0.3s ease;
  flex-shrink: 0;
  min-width: 120px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.techno-container span {
  font-weight: 500;
  font-size: 1rem;
  color: var(--text-primary);
  transition: color 0.3s ease;
}

.techno-container:hover {
  transform: translateY(-10px);
}

.techno-container:hover span {
  color: var(--emerald-primary);
}

.techno-icon {
  width: 60px;
  height: 60px;
  object-fit: contain;
  transition: all 0.3s ease;
  /* Les SVGs téléchargés ont déjà leurs couleurs */
}

.techno-container:hover .techno-icon {
  filter: brightness(1.2) saturate(1.2);
  transform: scale(1.1);
}

/* Animation d'apparition */
.skills {
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 1s ease-out forwards;
}

.section-title {
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.3s forwards;
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
@media screen and (max-width: 968px) {
  .skills {
    padding: 80px 15px;
  }

  #icons-list {
    gap: 50px;
  }

  .techno-container {
    min-width: 100px;
  }

  .techno-icon {
    width: 70px;
    height: 70px;
  }
}

@media screen and (max-width: 768px) {
  .skills {
    padding: 60px 10px;
  }

  .section-title {
    font-size: clamp(2rem, 4vw, 2.5rem);
    letter-spacing: 2px;
  }

  #icons-list {
    gap: 40px;
  }

  .techno-container {
    min-width: 90px;
    gap: 10px;
  }

  .techno-icon {
    width: 60px;
    height: 60px;
  }

  .techno-container span {
    font-size: 0.9rem;
  }
}

@media screen and (max-width: 480px) {
  .skills {
    padding: 50px 10px;
  }

  .section-title {
    font-size: 1.8rem;
    letter-spacing: 1px;
  }

  #icons-list {
    gap: 30px;
  }

  .techno-container {
    min-width: 80px;
  }

  .techno-icon {
    width: 50px;
    height: 50px;
  }

  .techno-container span {
    font-size: 0.8rem;
  }
}
</style>
