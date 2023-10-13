<template>
  <nav class="navbar navbar-expand-md navbar-light">
    <div class="container">
      <NuxtLink class="navbar-brand text-white" to="/">Home</NuxtLink>
      <div id="navbarSupportedContent" class="collapse navbar-collapse">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <NuxtLink class="navbar-brand nav-link active text-white" aria-current="page" to="/gear">All Gear</NuxtLink>
          </li>
          <li class="nav-item">
            <NuxtLink class="navbar-brand nav-link active text-white" aria-current="page" to="/about">About</NuxtLink>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<style scoped>
  .navbar{
    background-color: rgb(206, 102, 5);
  }
</style>