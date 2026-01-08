<script setup>

</script>

<template>
    <section class="skills" id="skills">
         <div class="container">
          <div class="section-header" data-aos="fade-up" data-aos-duration="1000">
              <h2 class="text-highlight-1 section-title">Mes technos préférées</h2>
          </div>
          <div class="scroll-wrapper">
            <div id="icons-list">
              <div class="techno-container"><i class="techno-icon devicon-html5-plain"></i> <br/> <span>HTML</span></div>
              <div class="techno-container"><i class="techno-icon devicon-css3-plain"></i> <br/> <span>CSS</span></div>
              <div class="techno-container"><i class="techno-icon devicon-javascript-plain"></i> <br/> <span>JS</span></div>
              <div class="techno-container"><i class="techno-icon devicon-mysql-original"></i> <br/> <span>SQL</span></div>
              <div class="techno-container"><i class="techno-icon devicon-csharp-plain"></i><br/> <span>C#</span></div>
              <div class="techno-container"><i class="techno-icon devicon-dot-net-plain"></i> <br/> <span>.net</span></div>
              <div class="techno-container"><i class="techno-icon devicon-vuetify-line"></i> <br/> <span>vuetify</span></div>
              <div class="techno-container"><i class="techno-icon devicon-docker-plain"></i> <br/> <span>Docker</span></div>
              <div class="techno-container"><i class="techno-icon devicon-git-plain"></i> <br/> <span>Git</span></div>
              <div class="techno-container"><i class="techno-icon devicon-bootstrap-plain"></i> <br/> <span>Bootstrap</span></div>
              <div class="techno-container"><i class="techno-icon devicon-tailwindcss-original"></i> <br/> <span>Tailwind</span></div>
              <div class="techno-container"><i class="techno-icon devicon-jquery-plain"></i> <br/> <span>jQuery</span></div>
              <div class="techno-container"><i class="techno-icon devicon-vuejs-plain"></i> <br/> <span>VueJS</span></div>
              <!-- Duplication pour effet infini -->
              <div class="techno-container"><i class="techno-icon devicon-html5-plain"></i> <br/> <span>HTML</span></div>
              <div class="techno-container"><i class="techno-icon devicon-css3-plain"></i> <br/> <span>CSS</span></div>
              <div class="techno-container"><i class="techno-icon devicon-javascript-plain"></i> <br/> <span>JS</span></div>
              <div class="techno-container"><i class="techno-icon devicon-mysql-original"></i> <br/> <span>SQL</span></div>
              <div class="techno-container"><i class="techno-icon devicon-csharp-plain"></i><br/> <span>C#</span></div>
              <div class="techno-container"><i class="techno-icon devicon-dot-net-plain"></i> <br/> <span>.net</span></div>
              <div class="techno-container"><i class="techno-icon devicon-vuetify-line"></i> <br/> <span>vuetify</span></div>
              <div class="techno-container"><i class="techno-icon devicon-docker-plain"></i> <br/> <span>Docker</span></div>
              <div class="techno-container"><i class="techno-icon devicon-unity-plain"></i> <br/> <span>Unity</span></div>
              <div class="techno-container"><i class="techno-icon devicon-git-plain"></i> <br/> <span>Git</span></div>
              <div class="techno-container"><i class="techno-icon devicon-bootstrap-plain"></i> <br/> <span>Bootstrap</span></div>
              <div class="techno-container"><i class="techno-icon devicon-tailwindcss-original"></i> <br/> <span>Tailwind</span></div>
              <div class="techno-container"><i class="techno-icon devicon-jquery-plain"></i> <br/> <span>jQuery</span></div>
              <div class="techno-container"><i class="techno-icon devicon-vuejs-plain"></i> <br/> <span>VueJS</span></div>
            </div>
          </div>
        </div>
      </section>
</template>

<style scoped>
  .skills {
    
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

.scroll-wrapper {
    overflow: hidden;
    width: 100%;
    margin-top: 35px;
}

#icons-list {
    display: flex;
    gap: 80px;
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
    color: var(--vt-c-custom-text-1); 
    transition: transform 0.5s;
    flex-shrink: 0;
    min-width: 120px;
}

.techno-container span {
    font-weight: bold;
}

.techno-container:hover {
    transform: rotate(15deg);
    color: var(--vt-c-custom-text-2);
}

.techno-icon {
    font-size: 80px;
    margin: 0 auto;
    color: white;
}

.techno-icon:hover {
    color: #ff6ec7;
    transform: rotate(15deg);
}

@media screen and (max-width: 905px) {
    #icons-list {
        gap: 60px;
    }
    
    .techno-container {
        min-width: 100px;
    }
    
    .techno-icon {
        font-size: 60px;
    }
}

@media screen and (max-width: 450px) {
    #icons-list {
        gap: 40px;
    }
    
    .techno-container {
        min-width: 80px;
    }
    
    .techno-icon {
        font-size: 50px;
    }
}
</style>