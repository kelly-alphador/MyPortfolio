<template>
  <section class="skills" id="skills">
    <div class="container">
      <div class="section-header" data-aos="fade-up" data-aos-duration="1000">
        <h2 class="section-title"> compétences</h2>
      </div>
      
      <div 
        class="scroll-area" 
        ref="scrollArea"
        @mousedown="startDrag"
        @touchstart="handleTouchStart"
      >
        <div 
          class="icons-container"
          ref="iconsContainer"
          :style="{ transform: `translateX(${scrollOffset}px)` }"
        >
          <!-- Liste originale -->
          <div 
            v-for="(tech, index) in technologies" 
            :key="index" 
            class="techno-container"
          >
            <img
              :src="getImageUrl(tech.icon)"
              :alt="tech.name"
              class="techno-icon"
            />
            <span>{{ tech.name }}</span>
          </div>
          
          <!-- Duplication pour l'effet infini -->
          <div 
            v-for="(tech, index) in technologies" 
            :key="'dup-' + index" 
            class="techno-container"
          >
            <img
              :src="getImageUrl(tech.icon)"
              :alt="tech.name"
              class="techno-icon"
            />
            <span>{{ tech.name }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Configuration des technologies
const technologies = [
  { name: 'HTML', icon: 'html.svg' },
  { name: 'CSS', icon: 'css.svg' },
  { name: 'JavaScript', icon: 'javascript.svg' },
  { name: 'C#', icon: 'csharp.svg' },
  { name: '.NET', icon: 'dotnet.svg' },
  { name: 'Vue.js', icon: 'vue.svg' },
  { name: 'MySQL', icon: 'mysql.svg' },
  { name: 'Docker', icon: 'docker.svg' },
  { name: 'Git', icon: 'git.svg' },
  { name: 'Bootstrap', icon: 'bootstrap.svg' },
  { name: 'Tailwind', icon: 'tailwind.svg' },
  { name: 'jQuery', icon: 'jquery.svg' },
]

const scrollArea = ref(null)
const iconsContainer = ref(null)
const scrollOffset = ref(0)
const autoScrollSpeed = ref(1)
const isDragging = ref(false)
const dragStartX = ref(0)
const dragStartOffset = ref(0)
const animationFrameId = ref(null)

// Fonction pour générer l'URL des images
const getImageUrl = (iconName) => {
  return new URL(`/src/assets/images/${iconName}`, import.meta.url).href
}

// Animation automatique
const animate = () => {
  if (!isDragging.value && iconsContainer.value) {
    scrollOffset.value -= autoScrollSpeed.value
    
    // Réinitialiser quand on arrive à la fin
    const containerWidth = iconsContainer.value.offsetWidth / 2
    if (Math.abs(scrollOffset.value) >= containerWidth) {
      scrollOffset.value = 0
    }
  }
  
  animationFrameId.value = requestAnimationFrame(animate)
}

// Démarrer le drag (desktop)
const startDrag = (e) => {
  if (e.type === 'mousedown') {
    isDragging.value = true
    dragStartX.value = e.clientX
    dragStartOffset.value = scrollOffset.value
    
    document.addEventListener('mousemove', onDragMove)
    document.addEventListener('mouseup', stopDrag)
    
    scrollArea.value?.classList.add('dragging')
    e.preventDefault()
  }
}

// Gestion du touch sur mobile
const handleTouchStart = (e) => {
  isDragging.value = true
  dragStartX.value = e.touches[0].clientX
  dragStartOffset.value = scrollOffset.value
  
  scrollArea.value?.addEventListener('touchmove', handleTouchMove, { passive: false })
  scrollArea.value?.addEventListener('touchend', handleTouchEnd)
  
  scrollArea.value?.classList.add('dragging')
}

const handleTouchMove = (e) => {
  if (!isDragging.value) return
  
  const touch = e.touches[0]
  const currentX = touch.clientX
  const deltaX = currentX - dragStartX.value
  
  scrollOffset.value = dragStartOffset.value + deltaX * 1.5
  
  if (Math.abs(deltaX) > 5) {
    e.preventDefault()
  }
}

const handleTouchEnd = () => {
  isDragging.value = false
  
  scrollArea.value?.removeEventListener('touchmove', handleTouchMove)
  scrollArea.value?.removeEventListener('touchend', handleTouchEnd)
  
  scrollArea.value?.classList.remove('dragging')
  
  setTimeout(() => {
    if (!isDragging.value) {
      autoScrollSpeed.value = 1
    }
  }, 2000)
}

// Pendant le drag (desktop)
const onDragMove = (e) => {
  if (!isDragging.value) return
  
  const currentX = e.clientX
  const deltaX = currentX - dragStartX.value
  scrollOffset.value = dragStartOffset.value + deltaX * 1.5
}

// Arrêter le drag (desktop)
const stopDrag = () => {
  isDragging.value = false
  
  document.removeEventListener('mousemove', onDragMove)
  document.removeEventListener('mouseup', stopDrag)
  
  scrollArea.value?.classList.remove('dragging')
  
  setTimeout(() => {
    if (!isDragging.value) {
      autoScrollSpeed.value = 1
    }
  }, 2000)
}

// Pause au survol (desktop seulement)
const pauseAutoScroll = () => {
  autoScrollSpeed.value = 0
}

const resumeAutoScroll = () => {
  if (!isDragging.value) {
    autoScrollSpeed.value = 1
  }
}

onMounted(() => {
  animate()
  
  scrollArea.value?.addEventListener('mouseenter', pauseAutoScroll)
  scrollArea.value?.addEventListener('mouseleave', resumeAutoScroll)
  
  if ('ontouchstart' in window) {
    autoScrollSpeed.value = 0.8
  }
})

onUnmounted(() => {
  if (animationFrameId.value) {
    cancelAnimationFrame(animationFrameId.value)
  }
  
  scrollArea.value?.removeEventListener('mouseenter', pauseAutoScroll)
  scrollArea.value?.removeEventListener('mouseleave', resumeAutoScroll)
})
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

/* Zone de défilement */
.scroll-area {
  position: relative;
  width: 100%;
  height: 200px;
  margin-top: 60px;
  overflow: hidden;
  user-select: none;
  -webkit-user-select: none;
  touch-action: pan-x pan-y;
}

.scroll-area.dragging {
  cursor: grabbing;
}

/* SUPPRIMÉ: Les dégradés verts sur les côtés */
/* .scroll-area::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100%;
  background: linear-gradient(
    90deg,
    rgba(80, 200, 120, 0.1) 0%,
    transparent 10%,
    transparent 90%,
    rgba(80, 200, 120, 0.1) 100%
  );
  pointer-events: none;
  z-index: 1;
} */

/* Indicateur texte */
.scroll-area::after {
  content: "← Glissez pour explorer →";
  position: absolute;
  bottom: -35px;
  left: 50%;
  transform: translateX(-50%);
  color: var(--emerald-primary);
  font-size: 0.9rem;
  opacity: 0;
  transition: opacity 0.3s ease;
  white-space: nowrap;
  z-index: 2;
}

.scroll-area:hover::after {
  opacity: 0.7;
}

/* Conteneur des icônes */
.icons-container {
  display: flex;
  gap: 60px;
  height: 100%;
  width: max-content;
  will-change: transform;
  transition: transform 0.1s linear;
  padding: 0 20px;
}

/* Style des technologies */
.techno-container {
  text-align: center;
  color: var(--text-secondary);
  transition: all 0.3s ease;
  flex-shrink: 0;
  min-width: 120px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  padding: 10px;
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
  pointer-events: none;
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

  .icons-container {
    gap: 50px;
  }

  .techno-container {
    min-width: 100px;
  }

  .techno-icon {
    width: 70px;
    height: 70px;
  }
  
  /* Toujours montrer l'indicateur sur mobile */
  .scroll-area::after {
    opacity: 0.8;
    animation: pulse 2s infinite;
    font-size: 0.85rem;
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

  .icons-container {
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
  
  .scroll-area {
    margin-top: 40px;
    height: 180px;
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

  .icons-container {
    gap: 30px;
    padding: 0 15px;
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
  
  .scroll-area {
    height: 160px;
    margin-top: 30px;
  }
  
  .scroll-area::after {
    font-size: 0.75rem;
    bottom: -30px;
  }
}

/* Support pour les appareils tactiles */
@media (hover: none) and (pointer: coarse) {
  .scroll-area {
    cursor: default;
  }
  
  .scroll-area.dragging {
    cursor: default;
  }
  
  .scroll-area::after {
    opacity: 0.8 !important;
    animation: pulse 2s infinite;
  }
  
  @keyframes pulse {
    0%, 100% { opacity: 0.6; }
    50% { opacity: 0.9; }
  }
  
  /* Désactiver les effets hover sur mobile */
  .techno-container:hover {
    transform: none;
  }
  
  .techno-container:hover span {
    color: var(--text-primary);
  }
  
  .techno-container:hover .techno-icon {
    filter: none;
    transform: none;
  }
}
</style>