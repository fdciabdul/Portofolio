<script setup lang="ts">
import { ref } from 'vue'
import { Icon } from '@iconify/vue'

const form = ref({
  name: '',
  email: '',
  subject: '',
  message: '',
})

const submitted = ref(false)

function submit() {
  submitted.value = true
  setTimeout(() => { submitted.value = false }, 3000)
  form.value = { name: '', email: '', subject: '', message: '' }
}

const contacts = [
  { icon: 'mdi:email', label: 'Email', value: 'taqin2731@gmail.com', href: 'mailto:taqin2731@gmail.com' },
  { icon: 'mdi:github', label: 'GitHub', value: 'github.com/fdciabdul', href: 'https://github.com/fdciabdul' },
  { icon: 'mdi:web', label: 'Blog', value: 'imtaqin.id', href: 'https://imtaqin.id' },
  { icon: 'mdi:whatsapp', label: 'WhatsApp', value: 'Chat on WhatsApp', href: '#' },
]
</script>

<template>
  <section id="contact" class="contact-section">
    <div class="container">
      <div class="contact-grid">
        <div class="contact-left">
          <span class="section-label section-label-light">Get In Touch</span>
          <h2 class="section-title contact-title">Let's Work Together</h2>
          <p class="contact-intro">
            Have a project in mind? Want to collaborate? Or just want to say hi?
            Drop me a message and I will get back to you within 24 hours.
          </p>

          <div class="contact-links">
            <a
              v-for="c in contacts"
              :key="c.label"
              :href="c.href"
              class="contact-link-card"
              target="_blank"
              rel="noopener"
            >
              <div class="contact-link-icon">
                <Icon :icon="c.icon" width="22" />
              </div>
              <div class="contact-link-text">
                <span class="contact-link-label">{{ c.label }}</span>
                <span class="contact-link-value">{{ c.value }}</span>
              </div>
              <Icon icon="mdi:arrow-right" width="18" class="contact-arrow" />
            </a>
          </div>
        </div>

        <div class="contact-right">
          <div class="contact-form-wrapper">
            <div v-if="submitted" class="success-msg">
              <Icon icon="mdi:check-circle" width="28" />
              Message sent! I will reply soon.
            </div>
            <form @submit.prevent="submit" class="contact-form">
              <div class="form-row">
                <div class="form-group">
                  <label for="name">Your Name</label>
                  <input
                    id="name"
                    v-model="form.name"
                    type="text"
                    placeholder="John Doe"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Email</label>
                  <input
                    id="email"
                    v-model="form.email"
                    type="email"
                    placeholder="john@example.com"
                    required
                  />
                </div>
              </div>
              <div class="form-group">
                <label for="subject">Subject</label>
                <input
                  id="subject"
                  v-model="form.subject"
                  type="text"
                  placeholder="Project Inquiry"
                  required
                />
              </div>
              <div class="form-group">
                <label for="message">Message</label>
                <textarea
                  id="message"
                  v-model="form.message"
                  rows="5"
                  placeholder="Tell me about your project..."
                  required
                ></textarea>
              </div>
              <button type="submit" class="neo-btn neo-btn-primary submit-btn">
                <Icon icon="mdi:send" width="18" />
                Send Message
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-section {
  background: var(--black);
  border-bottom: 3px solid var(--black);
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  align-items: start;
}

.section-label-light {
  background: var(--yellow);
  color: var(--black);
}

.contact-title {
  color: var(--white);
}

.contact-intro {
  font-family: Arial, sans-serif;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.75;
  color: rgba(255,255,255,0.6);
  margin-bottom: 2.5rem;
  margin-top: -1.5rem;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.contact-link-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  border: 2px solid rgba(255,255,255,0.2);
  padding: 0.875rem 1rem;
  color: var(--white);
  transition: all 0.1s;
  background: rgba(255,255,255,0.03);
}

.contact-link-card:hover {
  border-color: var(--yellow);
  background: rgba(158,255,0,0.05);
  transform: translateX(4px);
}

.contact-link-card:hover .contact-arrow {
  color: var(--yellow);
}

.contact-link-icon {
  width: 42px;
  height: 42px;
  background: var(--yellow);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--black);
  flex-shrink: 0;
}

.contact-link-text {
  display: flex;
  flex-direction: column;
  flex: 1;
}

.contact-link-label {
  font-size: 0.7rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.4);
}

.contact-link-value {
  font-size: 0.9rem;
  font-weight: 700;
  color: var(--white);
}

.contact-arrow {
  color: rgba(255,255,255,0.3);
  transition: color 0.1s;
}

.contact-form-wrapper {
  background: var(--white);
  border: 3px solid var(--yellow);
  box-shadow: 8px 8px 0 var(--yellow);
  padding: 2rem;
}

.success-msg {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  background: var(--lime);
  border: 2px solid var(--black);
  padding: 0.875rem 1rem;
  margin-bottom: 1.5rem;
  font-weight: 700;
  font-size: 0.9rem;
  text-transform: uppercase;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.375rem;
}

.form-group label {
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #555;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  font-family: inherit;
  font-size: 0.9rem;
  font-weight: 600;
  border: 2px solid var(--black);
  background: var(--bg);
  outline: none;
  transition: border-color 0.1s, box-shadow 0.1s;
  resize: vertical;
  color: var(--black);
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: var(--black);
  box-shadow: 3px 3px 0 var(--black);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #aaa;
  font-weight: 400;
}

.submit-btn {
  width: 100%;
  justify-content: center;
}

@media (max-width: 900px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}

@media (max-width: 520px) {
  .form-row {
    grid-template-columns: 1fr;
  }
}
</style>
