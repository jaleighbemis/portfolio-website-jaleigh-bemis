
<template>
  <div class="page">
    <header class="site-header">
      <h2>Jaleigh Bemis</h2>

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/portfolio">Portfolio</RouterLink>
      </nav>
    </header>

    <main>
      <RouterView />
    </main>

    <footer>
      <p>© 2026 Jaleigh Bemis</p>
    </footer>
  </div>
</template>
