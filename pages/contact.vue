<template>
  <div class="contact-page">
    <div class="contact-container">
      <h1 class="contact-title">Contactez-nous</h1>

      <form @submit.prevent="handleSubmit" class="contact-form">
        <div class="form-group">
          <label for="name">Nom</label>
          <input
              type="text"
              id="name"
              v-model="formData.name"
              required
              placeholder="Votre nom"
              class="form-input"
          />
        </div>

        <div class="form-group">
          <label for="email">Email</label>
          <input
              type="email"
              id="email"
              v-model="formData.email"
              required
              placeholder="votre@email.com"
              class="form-input"
          />
        </div>

        <div class="form-group">
          <label for="message">Message</label>
          <textarea
              id="message"
              v-model="formData.message"
              required
              rows="6"
              placeholder="Votre message..."
              class="form-input form-textarea"
          ></textarea>
        </div>

        <div class="form-actions">
          <button type="submit" class="btn btn-submit">Envoyer le message</button>
          <NuxtLink to="/" class="btn btn-back">Retour</NuxtLink>
        </div>
      </form>

      <Transition name="fade">
        <div v-if="submitted" class="success-message">
          <span class="icon">✨</span>
          Merci ! Votre message a été envoyé avec succès.
        </div>
      </Transition>
    </div>
  </div>
</template>

<script setup>
const formData = ref({
  name: '',
  email: '',
  message: ''
})

const submitted = ref(false)

const handleSubmit = () => {
  submitted.value = true
  setTimeout(() => {
    formData.value = { name: '', email: '', message: '' }
    submitted.value = false
  }, 3000)
}
</script>

<style scoped>
.contact-page {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 60px 20px;
  background: var(--bg-main);
}

.contact-container {
  background: var(--bg-card);
  border-radius: var(--radius-lg);
  padding: 60px;
  max-width: 700px;
  width: 100%;
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border);
}

.contact-title {
  text-align: center;
  margin-bottom: 50px;
  font-size: 3rem;
  font-weight: 800;
  background: var(--gradient-warm);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  letter-spacing: -0.02em;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

label {
  color: var(--text-main);
  font-weight: 600;
  font-size: 1.1rem;
  padding-left: 5px;
}

.form-input {
  padding: 18px 24px;
  border: 1.5px solid var(--border);
  border-radius: var(--radius-md);
  font-size: 1.1rem;
  font-family: 'Poppins', sans-serif;
  background: var(--bg-warm);
  color: var(--text-main);
  transition: var(--transition);
  box-shadow: inset 0 2px 4px rgba(0,0,0,0.02);
}

.form-input:focus {
  outline: none;
  border-color: var(--primary);
  background: white;
  box-shadow: 0 0 0 4px var(--primary-soft);
}

.form-textarea {
  resize: vertical;
  min-height: 160px;
}

.form-actions {
  display: flex;
  gap: 20px;
  margin-top: 20px;
}

.btn {
  padding: 18px 35px;
  font-size: 1.1rem;
  border-radius: 50px;
  cursor: pointer;
  text-decoration: none;
  text-align: center;
  transition: var(--transition);
  font-weight: 700;
}

.btn-submit {
  flex: 2;
  background: var(--gradient-warm);
  color: white;
  border: none;
  box-shadow: 0 10px 20px -5px rgba(242, 140, 107, 0.4);
}

.btn-submit:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 25px -5px rgba(242, 140, 107, 0.5);
}

.btn-back {
  flex: 1;
  background: white;
  color: var(--text-muted);
  border: 1px solid var(--border);
}

.btn-back:hover {
  background: var(--bg-warm);
  color: var(--text-main);
}

.success-message {
  margin-top: 30px;
  padding: 20px;
  background: #f0fdf4;
  color: #166534;
  border-radius: var(--radius-md);
  text-align: center;
  font-weight: 600;
  border: 1px solid #bbf7d0;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

@media (max-width: 768px) {
  .contact-container {
    padding: 40px 25px;
  }

  .contact-title {
    font-size: 2.2rem;
  }

  .form-actions {
    flex-direction: column;
  }
}
</style>