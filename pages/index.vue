<template>
  <div class="home-page">
    <div class="titles-container">
      <Transition name="fade">
        <h1 v-if="showTitle1" class="title title-1">Depuis quelques temps vous vous posez des questions ?</h1>
      </Transition>
      <Transition name="fade">
        <h2 v-if="showTitle2" class="title title-2">Je cherche le sens de ma vie</h2>
      </Transition>
      <Transition name="fade">
        <h2 v-if="showTitle3" class="title title-2">Ma vie n'a plus de sens</h2>
      </Transition>
      <Transition name="fade">
        <h2 v-if="showTitle4" class="title title-2"> J'ai un changement de vie... Comment retrouver le sens ?</h2>
      </Transition>
    </div>

    <Transition name="slide">
      <div v-if="showButtons" class="buttons-container">
        <NuxtLink to="/contact" class="btn btn-contact">Contact</NuxtLink>
        <NuxtLink to="/intro" class="btn btn-play">Commencer le Jeu</NuxtLink>
      </div>
    </Transition>
  </div>
</template>

<script setup>
const showTitle1 = ref(false)
const showTitle2 = ref(false)
const showTitle3 = ref(false)
const showTitle4 = ref(false)
const showTitle5 = ref(false)
const showButtons = ref(false)
onMounted(() => {
  setTimeout(() => showTitle1.value = true, 300)
  setTimeout(() => showTitle2.value = true, 1000)
  setTimeout(() => showTitle3.value = true, 1700)
  setTimeout(() => showTitle4.value = true, 2400)
  setTimeout(() => showButtons.value = true, 3100)
})
</script>

<style scoped>
.home-page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 40px;
  background: var(--bg-main);
}

.titles-container {
  text-align: center;
  margin-bottom: 60px;
}

.title {
  color: var(--text-main);
  margin: 20px 0;
  font-family: 'Poppins', sans-serif;
}

.title-1 {
  font-size: 3rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--text-muted);
}

.title-2 {
  font-size: 3rem;
  font-weight: 800;
  background: var(--gradient-warm);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-top: -10px;
}

.title-3 {
  font-size: 1.8rem;
  font-weight: 400;
  color: var(--text-light);
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.buttons-container {
  display: flex;
  gap: 30px;
  flex-wrap: wrap;
  justify-content: center;
}

.btn {
  padding: 20px 50px;
  font-size: 1.1rem;
  border-radius: 50px;
  cursor: pointer;
  text-decoration: none;
  transition: var(--transition);
  font-weight: 700;
}

.btn-contact {
  background: var(--bg-card);
  color: var(--text-main);
  border: 1px solid var(--border);
  box-shadow: var(--shadow-soft);
}

.btn-contact:hover {
  transform: translateY(-3px);
  background: white;
  box-shadow: var(--shadow-md);
}

.btn-play {
  background: var(--gradient-warm);
  color: white;
  box-shadow: 0 10px 20px -5px rgba(242, 140, 107, 0.4);
}

.btn-play:hover {
  transform: translateY(-3px);
  box-shadow: 0 20px 30px -5px rgba(242, 140, 107, 0.5);
}

@media (max-width: 768px) {
  .title-1 {
    font-size: 2.8rem;
  }

  .title-2 {
    font-size: 2.2rem;
  }

  .title-3 {
    font-size: 1.2rem;
  }

  .buttons-container {
    flex-direction: column;
    gap: 20px;
  }

  .btn {
    width: 100%;
    max-width: 300px;
  }
}
</style>