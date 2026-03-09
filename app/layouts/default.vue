<template>
  <div>
    <nav>
        <NuxtLink to="/">Accueil</NuxtLink>
        <NuxtLink to="/films">Films</NuxtLink>
        <NuxtLink to="/personnes">Personnes</NuxtLink>
    </nav>
    <Login/>
    <slot></slot>
  </div>
</template>