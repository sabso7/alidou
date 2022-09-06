<template>
<nav class="fixed px-2 sm:px-4 py-2.5 bg-transparent w-screen">
  <div class="container flex flex-wrap justify-between items-center mx-auto">
    <div class="rounded-full md:bg-emerald-700 drop-shadow-2xl">
      <a href="/" class="flex items-center">
        <img src="../assets/logo-alidou-menu-site.png" class="lg:h-20 h-12 rounded-lg m-2 md:block hidden" alt="alidou logo"/>
      </a>
    </div>
    
    <button data-collapse-toggle="navbar-default" type="button" class="bg-emerald-700 border-solid border-2 border-amber-700 rounded-full drop-shadow-2xl inline-flex items-center p-2 ml-3 text-4xl text-amber-600 md:hidden" aria-controls="navbar-default" aria-expanded="false">
      <span class="sr-only">Open main menu</span>
      <img src="../assets/Logo2.svg" class="h-12 p-2 rounded-lg m-2 md:hidden" alt="alidou logo"/>
    </button>
    <div class="hidden w-full md:block md:w-auto" id="navbar-default">
      <ul class="flex flex-col mt-4 md:flex-row md:space-x-8 md:mt-0 lg:text-lg lg:font-medium text-sm">
        <li>
          <nuxt-link to="/" class="block py-2 pr-4 pl-3 text-emerald-700 rounded md:bg-transparent dark:text-emerald-700 comFont" aria-current="page">Accueil</nuxt-link>
        </li>
          <nuxt-link to="/carte" class="block py-2 pr-4 pl-3 text-emerald-700 rounded md:bg-transparent dark:text-emerald-700 comFont" aria-current="page">Carte</nuxt-link>
        <li>
          <nuxt-link to="/event" class="block py-2 pr-4 pl-3 text-emerald-700 rounded md:bg-transparent dark:text-emerald-700 comFont" aria-current="page">Expositions</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/workshop" class="block py-2 pr-4 pl-3 text-emerald-700 rounded md:bg-transparent dark:text-emerald-700 comFont" aria-current="page">Ateliers</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/about" class="block py-2 pr-4 pl-3 text-emerald-700 rounded md:bg-transparent dark:text-emerald-700 comFont" aria-current="page">A propos</nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</nav>
</template>