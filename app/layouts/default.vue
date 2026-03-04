<template>
  <div>
    <nav>
        <NuxtLink to="/">Accueil</NuxtLink>
        <NuxtLink to="/films">Films</NuxtLink>
    </nav>
    <Login/>
    <slot></slot>
  </div>
</template>