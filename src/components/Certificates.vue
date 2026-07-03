<template>
  <section class="certif-section">
    <div class="certif-container">
      <!-- Header -->
      <div class="certif-header">
        <span class="certif-eyebrow">Preuves & parcours</span>
        <h2 class="certif-title">Certificats & Attestations</h2>
        <p class="certif-subtitle">
          Ce que j'ai appris, validé et pratiqué — en stage comme en autoformation.
        </p>
      </div>

      <!-- Tabs -->
      <div class="certif-tabs">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          class="certif-tab"
          :class="{ active: activeTab === tab.id }"
          @click="activeTab = tab.id"
        >
          {{ tab.label }}
          <span class="certif-count">{{ countFor(tab.id) }}</span>
        </button>
        <div class="certif-tab-indicator" :style="indicatorStyle"></div>
      </div>

      <!-- Grid -->
      <transition-group name="certif-fade" tag="div" class="certif-grid">
        <div
          v-for="item in filteredItems"
          :key="item.id"
          class="certif-card"
          @click="downloadCertificate(item)"
        >
          <div class="certif-thumb">
            <iframe
              v-if="item.file"
              :src="item.file + '#toolbar=0&navpanes=0&view=FitH'"
              class="certif-pdf-preview"
              tabindex="-1"
            ></iframe>
            <div class="certif-thumb-overlay">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                <path
                  d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4M7 10l5 5 5-5M12 15V3"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                />
              </svg>
              <span>Télécharger le certificat</span>
            </div>
            <span class="certif-badge" :class="item.type">{{
              item.type === "stage" ? "Stage" : "Udemy"
            }}</span>
          </div>

          <div class="certif-body">
            <h3 class="certif-card-title">{{ item.title }}</h3>
            <p class="certif-issuer">{{ item.issuer }}</p>
            <div class="certif-meta">
              <span class="certif-date">{{ item.date }}</span>
              <span v-if="item.duration" class="certif-dot">•</span>
              <span v-if="item.duration" class="certif-duration">{{
                item.duration
              }}</span>
            </div>
          </div>
        </div>
      </transition-group>

      <p v-if="filteredItems.length === 0" class="certif-empty">
        Aucun élément à afficher pour l'instant.
      </p>
    </div>
  </section>
</template>

<script>
// Import direct des PDF depuis assets pour que Vite les inclue dans le build
// (adapte le chemin si tu n'utilises pas l'alias "@" -> vérifie jsconfig.json)
import attestationPdf from "@/assets/pdf/attestation.pdf";
import certPdf from "@/assets/pdf/cert.pdf";

export default {
  name: "Certificates",
  data() {
    return {
      activeTab: "all",
      tabs: [
        { id: "all", label: "Tout" },
        { id: "stage", label: "Attestations de stage" },
        { id: "udemy", label: "Certificats Udemy" },
      ],
      // ⚠️ Ajuste titre / organisme / date pour qu'ils correspondent à tes vrais documents.
      items: [
        {
          id: 1,
          type: "stage",
          title: "Attestation de stage",
          issuer: "SMART SYSTEMS , Tunis",
          date: "2026",
          duration: "",
          file: attestationPdf,
        },
        {
          id: 2,
          type: "udemy",
          title: "Certificat Udemy",
          issuer: "Udemy",
          date: "2026",
          duration: "",
          file: certPdf,
        },
      ],
    };
  },
  computed: {
    filteredItems() {
      if (this.activeTab === "all") return this.items;
      return this.items.filter((i) => i.type === this.activeTab);
    },
    indicatorStyle() {
      const index = this.tabs.findIndex((t) => t.id === this.activeTab);
      return {
        transform: `translateX(${index * 100}%)`,
        width: `${100 / this.tabs.length}%`,
      };
    },
  },
  methods: {
    countFor(tabId) {
      if (tabId === "all") return this.items.length;
      return this.items.filter((i) => i.type === tabId).length;
    },
    downloadCertificate(item) {
      if (!item.file) return;
      const link = document.createElement("a");
      link.href = item.file;
      link.download = `${item.title.replace(/\s+/g, "_")}.pdf`;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    },
  },
};
</script>

<style scoped>
.certif-section {
  width: 100%;
  padding: 100px 20px;
  position: relative;
}

.certif-container {
  max-width: 1200px;
  margin: 0 auto;
}

.certif-header {
  text-align: center;
  margin-bottom: 50px;
}

.certif-eyebrow {
  display: inline-block;
  font-size: 0.85rem;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--emerald-primary);
  font-weight: 600;
  margin-bottom: 12px;
}

.certif-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 12px;
}

.certif-subtitle {
  color: var(--text-secondary);
  font-size: 1.05rem;
  opacity: 0.8;
  max-width: 520px;
  margin: 0 auto;
}

/* Tabs */
.certif-tabs {
  position: relative;
  display: flex;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(80, 200, 120, 0.15);
  border-radius: 12px;
  padding: 6px;
  max-width: 620px;
  margin: 0 auto 45px;
}

.certif-tab {
  flex: 1;
  position: relative;
  z-index: 2;
  background: none;
  border: none;
  color: var(--text-secondary);
  font-family: inherit;
  font-size: 0.95rem;
  font-weight: 500;
  padding: 10px 14px;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  transition: color 0.3s ease;
}

.certif-tab.active {
  color: var(--bg-dark);
}

.certif-count {
  font-size: 0.75rem;
  background: rgba(255, 255, 255, 0.12);
  padding: 1px 7px;
  border-radius: 10px;
}

.certif-tab.active .certif-count {
  background: rgba(10, 12, 10, 0.2);
}

.certif-tab-indicator {
  position: absolute;
  top: 6px;
  left: 6px;
  bottom: 6px;
  background: linear-gradient(135deg, var(--emerald-primary), var(--emerald-dark));
  border-radius: 8px;
  transition: transform 0.35s cubic-bezier(0.34, 1.56, 0.64, 1);
  z-index: 1;
  width: calc(33.333% - 4px);
}

/* Grid */
.certif-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 28px;
}

.certif-card {
  background: rgba(22, 25, 22, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 14px;
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.certif-card:hover {
  transform: translateY(-6px);
  border-color: rgba(80, 200, 120, 0.4);
  box-shadow: 0 15px 35px rgba(80, 200, 120, 0.15);
}

.certif-thumb {
  position: relative;
  width: 100%;
  aspect-ratio: 4 / 3;
  background: rgba(80, 200, 120, 0.06);
  overflow: hidden;
}

.certif-pdf-preview {
  position: absolute;
  top: 0;
  left: 0;
  width: 133%;
  height: 133%;
  border: none;
  pointer-events: none;
  background: #fff;
  transform: scale(0.9) translateY(-4%);
  transform-origin: top left;
  transition: transform 0.4s ease;
}

.certif-card:hover .certif-pdf-preview {
  transform: scale(0.94) translateY(-4%);
}

.certif-thumb-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--emerald-primary);
  opacity: 0.5;
}

.certif-thumb-overlay {
  position: absolute;
  inset: 0;
  background: rgba(10, 12, 10, 0.75);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  opacity: 0;
  transition: opacity 0.3s ease;
  color: var(--emerald-primary);
  font-weight: 600;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  text-align: center;
  padding: 0 12px;
}

.certif-card:hover .certif-thumb-overlay {
  opacity: 1;
}

.certif-badge {
  position: absolute;
  top: 12px;
  left: 12px;
  font-size: 0.7rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  padding: 4px 10px;
  border-radius: 20px;
  backdrop-filter: blur(6px);
}

.certif-badge.stage {
  background: rgba(80, 200, 120, 0.85);
  color: var(--bg-dark);
}

.certif-badge.udemy {
  background: rgba(236, 90, 43, 0.85);
  color: #fff;
}

.certif-body {
  padding: 18px 20px 22px;
}

.certif-card-title {
  font-size: 1.05rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 6px;
  line-height: 1.35;
}

.certif-issuer {
  color: var(--emerald-primary);
  font-size: 0.9rem;
  font-weight: 500;
  margin-bottom: 8px;
}

.certif-meta {
  display: flex;
  align-items: center;
  gap: 6px;
  color: var(--text-secondary);
  font-size: 0.82rem;
  opacity: 0.75;
}

.certif-empty {
  text-align: center;
  color: var(--text-secondary);
  opacity: 0.6;
  padding: 40px 0;
}

/* Transitions grille */
.certif-fade-enter-active,
.certif-fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}
.certif-fade-enter-from,
.certif-fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}

@media (max-width: 768px) {
  .certif-section {
    padding: 70px 15px;
  }
  .certif-title {
    font-size: 1.9rem;
  }
  .certif-tabs {
    flex-wrap: wrap;
  }
  .certif-tab {
    font-size: 0.85rem;
    padding: 9px 8px;
  }
  .certif-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}
</style>