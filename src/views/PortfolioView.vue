
<script setup>
import { ref, onMounted } from 'vue'

const repositories = ref([])
const loading = ref(true)
const error = ref('')

async function fetchRepositories() {
  try {
    const response = await fetch(
      'https://api.github.com/users/jaleighbemis/repos?sort=updated&per_page=100'
    )

    if (!response.ok) {
      throw new Error('Unable to load repositories')
    }

    repositories.value = await response.json()
  } catch (err) {
    error.value = 'Sorry, my projects could not be loaded right now. Please try again later.'
  } finally {
    loading.value = false
  }
}

function formatDate(date) {
  return new Date(date).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  })
}

onMounted(fetchRepositories)
</script>

<template>
  <section class="content-section portfolio-section">
    <p class="eyebrow">My Work</p>
    <h1>My Portfolio</h1>

    <p>
      Here are some of the projects I've worked on while
      learning programming and web development.
      These projects are automatically updated from GitHub.
    </p>

    <p v-if="loading">Loading my projects...</p>

    <p v-else-if="error" class="error-message">
      {{ error }}
    </p>

    <p v-else-if="repositories.length === 0">
      No public repositories to display yet.
    </p>

    <div v-else class="repo-grid">
      <div
        v-for="repo in repositories"
        :key="repo.id"
        class="repo-card"
      >
        <h2>
          <a :href="repo.html_url" target="_blank" rel="noopener noreferrer">
            {{ repo.name }}
          </a>
        </h2>

        <p>
          {{ repo.description || 'No description available.' }}
        </p>

        <p>
          <strong>Language:</strong>
          {{ repo.language || 'Not specified' }}
        </p>

        <p>
          <strong>Last Updated:</strong>
          {{ formatDate(repo.updated_at) }}
        </p>
      </div>
    </div>
  </section>
</template>
