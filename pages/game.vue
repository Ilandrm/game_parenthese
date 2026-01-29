<template>
  <div class="game-page">
    <h2 class="round-title">{{ rounds[currentRound].title }}</h2>

    <div v-if="gameState === 'select'" class="select-card-view">

      <div class="coach-image-container">
        <img
            :src="`/images/etatjeux/state${currentRound + 1}.jpg`"
            alt="Coach & Sens"
            class="coach-image"
        />
      </div>

      <div class="cards-container">
        <div
            v-for="(card, index) in 5"
            :key="index"
            @click="selectCard(index)"
            class="card card-back"
        >
          <div class="card-placeholder">
            <span>?</span>
          </div>
        </div>
      </div>
    </div>

    <div v-else-if="gameState === 'video'" class="card-reveal-view">
      <div class="content-grid">
        <div class="card-section">
          <img
              :src="selectedCardImage"
              :alt="rounds[currentRound].title"
              class="revealed-card"
          />
        </div>

        <div class="video-section">
          <div class="video-placeholder">
            <span>Vidéo</span>
          </div>
        </div>
      </div>

      <button @click="nextStep" class="btn btn-next">Passer</button>
    </div>

    <div v-else-if="gameState === 'text'" class="text-input-view">
      <div class="content-grid">
        <div class="card-section">
          <img
              :src="selectedCardImage"
              :alt="rounds[currentRound].title"
              class="revealed-card"
          />
        </div>

        <div class="text-section">
          <textarea
              v-model="userText"
              placeholder="Écrivez vos réflexions ici..."
              class="text-input"
          ></textarea>
        </div>
      </div>

      <button @click="continueGame" class="btn btn-next" :disabled="userText === ''">Continuer</button>
    </div>

    <div v-else-if="gameState === 'end'" class="end-view">
      <h2>Félicitations !</h2>
      <p>Vous avez terminé le jeu de bien-être</p>
      <NuxtLink to="/" class="btn btn-home">Retour à l'accueil</NuxtLink>
    </div>
  </div>
</template>

<script setup>
const rounds = [
  { title: 'Clarifier', image: '/images/clarifier.jpg' },
  { title: 'Ressentir', image: '/images/ressentir.jpg' },
  { title: 'Histoire Personnelle', image: '/images/placeholder-card.jpg' },
  { title: 'Contribution Joie', image: '/images/placeholder-card.jpg' }
]

const currentRound = ref(0)
const gameState = ref('select')
const selectedCardImage = ref('')
const userText = ref('')

const selectCard = (index) => {
  selectedCardImage.value = rounds[currentRound.value].image
  gameState.value = 'video'
}

const nextStep = () => {
  gameState.value = 'text'
}

const continueGame = () => {
  userText.value = ''

  if (currentRound.value < rounds.length - 1) {
    currentRound.value++
    gameState.value = 'select'
  } else {
    gameState.value = 'end'
  }
}
</script>

<style scoped>
.game-page {
  min-height: 100vh;
  padding: 60px 20px;
  background: var(--bg-main);
}

.select-card-view {
  max-width: 1200px;
  margin: 0 auto;
}

.round-title {
  text-align: center;
  color: var(--text-main);
  font-size: 3rem;
  margin-bottom: 50px;
  font-weight: 800;
  letter-spacing: -0.02em;
}

.coach-image-container {
  display: flex;
  justify-content: center;
  margin-bottom: 50px;
}

.coach-image {
  max-width: 600px;
  width: 100%;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  border: 4px solid white;
}

.cards-container {
  display: flex;
  justify-content: center;
  gap: 25px;
  flex-wrap: wrap;
}

.card {
  width: 160px;
  height: 240px;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: var(--transition);
  box-shadow: var(--shadow-soft);
  border: 1px solid var(--border);
}

.card:hover {
  transform: translateY(-12px) scale(1.05);
  box-shadow: var(--shadow-md);
}

.card-back {
  background: var(--gradient-warm);
  display: flex;
  justify-content: center;
  align-items: center;
}

.card-placeholder {
  color: white;
  font-size: 4.5rem;
  font-weight: 700;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.card-reveal-view,
.text-input-view {
  max-width: 1200px;
  margin: 0 auto;
}

.content-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 50px;
  margin-bottom: 50px;
}

.card-section,
.video-section,
.text-section {
  display: flex;
  justify-content: center;
  align-items: center;
}

.revealed-card {
  max-width: 100%;
  height: 600px;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  border: 4px solid white;
}

.video-placeholder {
  width: 100%;
  aspect-ratio: 16/9;
  background: var(--bg-card);
  border-radius: var(--radius-lg);
  display: flex;
  justify-content: center;
  align-items: center;
  color: var(--text-muted);
  font-size: 2.2rem;
  font-weight: 700;
  border: 3px dashed var(--border);
}

.text-input {
  width: 100%;
  min-height: 350px;
  padding: 30px;
  border-radius: var(--radius-lg);
  border: 1.5px solid var(--border);
  background: var(--bg-card);
  font-size: 1.2rem;
  font-family: 'Poppins', sans-serif;
  color: var(--text-main);
  resize: vertical;
  box-shadow: var(--shadow-soft);
  transition: var(--transition);
}

.text-input:focus {
  outline: none;
  border-color: var(--primary);
  background: white;
  box-shadow: 0 0 0 4px var(--primary-soft);
}

.btn-next,
.btn-home {
  display: block;
  margin: 0 auto;
  padding: 20px 70px;
  font-size: 1.4rem;
  background: var(--gradient-warm);
  color: white;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  text-decoration: none;
  transition: var(--transition);
  font-weight: 700;
  box-shadow: 0 10px 20px -5px rgba(242, 140, 107, 0.4);
}

.btn-next:hover:not(:disabled),
.btn-home:hover {
  transform: translateY(-4px);
  box-shadow: 0 15px 30px -5px rgba(242, 140, 107, 0.5);
}

.btn-next:disabled {
  background: var(--text-light);
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
  opacity: 0.5;
}

.end-view {
  text-align: center;
  padding: 100px 20px;
}

.end-view h2 {
  color: var(--text-main);
  font-size: 3.5rem;
  margin-bottom: 20px;
  font-weight: 800;
}

.end-view p {
  color: var(--text-muted);
  font-size: 1.6rem;
  margin-bottom: 50px;
}

@media (max-width: 968px) {
  .content-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .card {
    width: 140px;
    height: 210px;
  }
}

@media (max-width: 768px) {
  .round-title {
    font-size: 2.2rem;
  }

  .card {
    width: 120px;
    height: 180px;
  }

  .card-placeholder {
    font-size: 3.5rem;
  }
}
</style>