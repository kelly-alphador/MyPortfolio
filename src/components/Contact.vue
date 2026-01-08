<template>
  <section class="contact" id="contact">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">CONTACTEZ-MOI</h2>
      </div>

      <div class="contact-content">
        <!-- Informations de contact -->
        <div class="contact-info">
          <div class="contact-item">
            <div class="contact-icon">
              <svg
                width="24"
                height="24"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                ></path>
              </svg>
            </div>
            <div class="contact-details">
              <h3 class="contact-label">Email</h3>
              <p class="contact-value">kellyalphador@gmail.com</p>
            </div>
          </div>

          <div class="contact-item">
            <div class="contact-icon">
              <svg
                width="24"
                height="24"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
                ></path>
              </svg>
            </div>
            <div class="contact-details">
              <h3 class="contact-label">Téléphone</h3>
              <p class="contact-value">034 52 383 97</p>
            </div>
          </div>

          <div class="contact-item">
            <div class="contact-icon">
              <svg
                width="24"
                height="24"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                ></path>
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                ></path>
              </svg>
            </div>
            <div class="contact-details">
              <h3 class="contact-label">Localisation</h3>
              <p class="contact-value">Fianarantsoa, Madagascar</p>
            </div>
          </div>
        </div>

        <!-- Formulaire de contact -->
        <div class="contact-form-container">
          <form @submit.prevent="submitForm" class="contact-form">
            <div class="form-group">
              <label for="name">Nom complet</label>
              <input
                type="text"
                id="name"
                v-model="form.name"
                :class="{ error: errors.name }"
                placeholder="Votre nom complet"
                required
              />
              <span v-if="errors.name" class="error-message">{{
                errors.name
              }}</span>
            </div>

            <div class="form-group">
              <label for="email">Email</label>
              <input
                type="email"
                id="email"
                v-model="form.email"
                :class="{ error: errors.email }"
                placeholder="votre@email.com"
                required
              />
              <span v-if="errors.email" class="error-message">{{
                errors.email
              }}</span>
            </div>

            <div class="form-group">
              <label for="subject">Sujet</label>
              <input
                type="text"
                id="subject"
                v-model="form.subject"
                :class="{ error: errors.subject }"
                placeholder="Sujet de votre message"
                required
              />
              <span v-if="errors.subject" class="error-message">{{
                errors.subject
              }}</span>
            </div>

            <div class="form-group">
              <label for="message">Message</label>
              <textarea
                id="message"
                v-model="form.message"
                :class="{ error: errors.message }"
                placeholder="Décrivez votre projet ou votre demande..."
                rows="4"
                required
              ></textarea>
              <span v-if="errors.message" class="error-message">{{
                errors.message
              }}</span>
            </div>

            <button
              type="submit"
              class="submit-btn"
              :disabled="isSubmitting"
              :class="{ submitting: isSubmitting }"
            >
              <span v-if="!isSubmitting">Envoyer le message</span>
              <span v-else>
                <svg class="spinner" width="20" height="20" viewBox="0 0 24 24">
                  <circle
                    cx="12"
                    cy="12"
                    r="10"
                    stroke="currentColor"
                    stroke-width="4"
                    fill="none"
                    opacity="0.3"
                  />
                  <path
                    d="M12 2a10 10 0 0 1 10 10"
                    stroke="currentColor"
                    stroke-width="4"
                    fill="none"
                  />
                </svg>
                Envoi en cours...
              </span>
            </button>
          </form>

          <div
            v-if="submitStatus"
            class="submit-status"
            :class="submitStatus.type"
          >
            <div class="status-icon">
              <svg
                v-if="submitStatus.type === 'success'"
                width="20"
                height="20"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M5 13l4 4L19 7"
                ></path>
              </svg>
              <svg
                v-else
                width="20"
                height="20"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M6 18L18 6M6 6l12 12"
                ></path>
              </svg>
            </div>
            <span>{{ submitStatus.message }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Contact",
  data() {
    return {
      form: {
        name: "",
        email: "",
        subject: "",
        message: "",
      },
      errors: {},
      isSubmitting: false,
      submitStatus: null,
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

      document.querySelectorAll(".contact-item").forEach((item) => {
        observer.observe(item);
      });
    },

    validateForm() {
      this.errors = {};

      if (!this.form.name.trim()) {
        this.errors.name = "Le nom est requis";
      } else if (this.form.name.trim().length < 2) {
        this.errors.name = "Le nom doit contenir au moins 2 caractères";
      }

      if (!this.form.email.trim()) {
        this.errors.email = "L'email est requis";
      } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.form.email)) {
        this.errors.email = "Format d'email invalide";
      }

      if (!this.form.subject.trim()) {
        this.errors.subject = "Le sujet est requis";
      }

      if (!this.form.message.trim()) {
        this.errors.message = "Le message est requis";
      } else if (this.form.message.trim().length < 10) {
        this.errors.message = "Le message doit contenir au moins 10 caractères";
      }

      return Object.keys(this.errors).length === 0;
    },

    async submitForm() {
      if (!this.validateForm()) {
        return;
      }

      this.isSubmitting = true;
      this.submitStatus = null;

      try {
        await new Promise((resolve) => setTimeout(resolve, 2000));

        this.submitStatus = {
          type: "success",
          message:
            "Message envoyé avec succès ! Je vous répondrai dans les plus brefs délais.",
        };

        this.form = {
          name: "",
          email: "",
          subject: "",
          message: "",
        };
      } catch (error) {
        this.submitStatus = {
          type: "error",
          message: "Erreur lors de l'envoi du message. Veuillez réessayer.",
        };
      } finally {
        this.isSubmitting = false;

        setTimeout(() => {
          this.submitStatus = null;
        }, 5000);
      }
    },
  },
};
</script>

<style scoped>
/* Import de la police Syncopate */
@import url("https://fonts.googleapis.com/css2?family=Syncopate:wght@400;500;700&display=swap");

/* Variables */
.contact {
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
  font-weight: 500;
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  color: var(--emerald-primary);
  letter-spacing: 3px;
  text-transform: uppercase;
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

/* Layout desktop */
.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

/* Informations de contact */
.contact-info {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  opacity: 0;
  transform: translateX(-20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.contact-item.animated {
  opacity: 1;
  transform: translateX(0);
}

.contact-icon {
  color: var(--emerald-primary);
  flex-shrink: 0;
}

.contact-details {
  flex: 1;
}

.contact-label {
  color: var(--emerald-primary);
  font-size: 0.9rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 0.25rem;
}

.contact-value {
  color: var(--text-primary);
  font-size: 1rem;
  font-weight: 400;
}

/* Liens sociaux */
.social-links {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.social-link {
  color: var(--text-muted);
  transition: all 0.3s ease;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 6px;
}

.social-link:hover {
  color: var(--emerald-primary);
  background: rgba(80, 200, 120, 0.1);
  transform: translateY(-2px);
}

/* Formulaire de contact */
.contact-form-container {
  width: 100%;
}

.contact-form {
  width: 100%;
}

.form-group {
  margin-bottom: 2rem;
}

.form-group label {
  display: block;
  color: var(--text-primary);
  font-size: 0.9rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  background: transparent;
  border: none;
  border-bottom: 1px solid rgba(80, 200, 120, 0.3);
  color: var(--text-primary);
  font-size: 1rem;
  padding: 0.5rem 0;
  transition: all 0.3s ease;
  resize: vertical;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: var(--text-muted);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-bottom-color: var(--emerald-primary);
}

.form-group input.error,
.form-group textarea.error {
  border-bottom-color: #ff6b6b;
}

.error-message {
  display: block;
  color: #ff6b6b;
  font-size: 0.8rem;
  margin-top: 0.5rem;
}

.submit-btn {
  background: var(--emerald-primary);
  color: #161916;
  border: none;
  padding: 0.75rem 2rem;
  font-size: 0.9rem;
  font-weight: 600;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  width: 100%;
}

.submit-btn:hover:not(:disabled) {
  background: var(--emerald-dark);
  transform: translateY(-2px);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.submit-btn.submitting {
  background: var(--emerald-dark);
}

.spinner {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.submit-status {
  margin-top: 1.5rem;
  padding: 1rem;
  border-radius: 6px;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 0.9rem;
}

.submit-status.success {
  background: rgba(34, 197, 94, 0.1);
  color: #22c55e;
}

.submit-status.error {
  background: rgba(255, 107, 107, 0.1);
  color: #ff6b6b;
}

.status-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Animations décalées pour chaque item */
.contact-item:nth-child(1).animated {
  animation: fadeInLeft 0.6s ease 0.1s forwards;
}

.contact-item:nth-child(2).animated {
  animation: fadeInLeft 0.6s ease 0.2s forwards;
}

.contact-item:nth-child(3).animated {
  animation: fadeInLeft 0.6s ease 0.3s forwards;
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* RESPONSIVE DESIGN */
@media (max-width: 1100px) {
  .contact-content {
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
  }
}

@media (max-width: 768px) {
  .contact {
    padding: 80px 15px;
  }

  .section-header {
    margin-bottom: 3rem;
  }

  .section-title {
    font-size: clamp(2rem, 4vw, 2.5rem);
    letter-spacing: 2px;
  }

  .contact-content {
    grid-template-columns: 1fr;
    gap: 3rem;
    max-width: 500px;
    margin: 0 auto;
  }

  .contact-info {
    gap: 1.5rem;
  }

  .contact-item {
    gap: 0.75rem;
  }

  .contact-label {
    font-size: 0.85rem;
  }

  .contact-value {
    font-size: 0.9rem;
  }

  .social-links {
    justify-content: center;
    margin-top: 1.5rem;
  }

  .form-group {
    margin-bottom: 1.5rem;
  }

  .form-group input,
  .form-group textarea {
    font-size: 0.9rem;
  }

  .submit-btn {
    padding: 0.625rem 1.5rem;
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .contact {
    padding: 60px 10px;
  }

  .section-title {
    font-size: 1.8rem;
    letter-spacing: 1px;
  }

  .contact-content {
    gap: 2rem;
  }

  .contact-item {
    flex-direction: column;
    gap: 0.5rem;
  }

  .contact-label {
    font-size: 0.8rem;
  }

  .contact-value {
    font-size: 0.85rem;
  }

  .social-links {
    gap: 0.75rem;
  }

  .social-link {
    width: 32px;
    height: 32px;
  }

  .form-group input,
  .form-group textarea {
    font-size: 0.85rem;
  }

  .submit-btn {
    padding: 0.5rem 1.25rem;
    font-size: 0.8rem;
  }

  .submit-status {
    padding: 0.75rem;
    font-size: 0.85rem;
  }
}
</style>
