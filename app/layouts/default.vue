<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Navigation Bar -->
    <nav class="flex justify-center gap-6 bg-white p-6 shadow-sm">
      <NuxtLink to="/" class="font-medium text-gray-600 hover:text-blue-600">
        Home
      </NuxtLink>
      <NuxtLink
        to="/about"
        class="font-medium text-gray-600 hover:text-blue-600"
      >
        About
      </NuxtLink>
      <NuxtLink
        to="/register"
        class="font-medium text-gray-600 hover:text-blue-600"
        >Register</NuxtLink
      >
      <!-- Nuxt intercetta il click e cambia pagina istantaneamente usando JavaScript (Client-Side Rendering), senza ricaricare l'intero sito nel browser.-->
      <!--Se per caso Nuxt nota che un utente sta per cliccare su un link, pre-carica i dati di quella pagina in background, rendendo la navigazione molto più fluida.-->
    </nav>

    <!-- Punto preciso in cui saranno inseriti e mostrati i Contenuti delle pagine, slot=segnaposto -->
    <main class="p-10">
      <slot></slot>
    </main>
  </div>
</template>
