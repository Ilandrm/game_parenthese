<template>
  <div class="intro-page">
    <div class="intro-container">
      <div class="image-wrapper">
        <img
            src="/images/etatjeux/state1.jpg"
            alt="Coach & Sens"
            class="intro-image"
        />
      </div>
      <NuxtLink to="/game" class="btn btn-start">
        Commencer l'expérience
        <span class="arrow">→</span>
      </NuxtLink>
    </div>
  </div>
</template>

<style scoped>
.intro-page {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 60px 20px;
  background: var(--bg-main);
}

.intro-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 50px;
  max-width: 900px;
  width: 100%;
}

.image-wrapper {
  width: 100%;
  padding: 15px;
  background: white;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border);
}

.intro-image {
  width: 100%;
  display: block;
  border-radius: calc(var(--radius-lg) - 10px);
  transition: var(--transition);
}

.image-wrapper:hover .intro-image {
  transform: scale(1.01);
}

.btn-start {
  padding: 22px 80px;
  font-size: 1.4rem;
  background: var(--gradient-warm);
  color: white;
  border: none;
  border-radius: 60px;
  cursor: pointer;
  text-decoration: none;
  transition: var(--transition);
  font-weight: 700;
  box-shadow: 0 15px 30px -10px rgba(242, 140, 107, 0.5);
  display: flex;
  align-items: center;
  gap: 15px;
}

.btn-start:hover {
  transform: translateY(-5px);
  box-shadow: 0 25px 40px -10px rgba(242, 140, 107, 0.6);
}

.arrow {
  transition: transform 0.3s ease;
}

.btn-start:hover .arrow {
  transform: translateX(8px);
}

@media (max-width: 768px) {
  .intro-container {
    gap: 35px;
  }

  .btn-start {
    width: 100%;
    padding: 20px 40px;
    font-size: 1.2rem;
    justify-content: center;
  }
}
</style>