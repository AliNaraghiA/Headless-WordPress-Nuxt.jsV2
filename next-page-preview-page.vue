<template>
  <div>
    <ul>
      <li v-if="page > 1">
        <nuxt-link :to="{ path: $route.path, query: { page: page - 1 } }">Prev</nuxt-link>
      </li>
      <li v-for="n in totalPages" :key="n :class="{ active: n === page }">
        <nuxt-link :to="{ path: $route.path, query: { page: n } }">{{ n }}</nuxt-link>
      </li>
      <li v-if="page < totalPages">
        <nuxt-link :to="{ path: $route.path, query: { page: page + 1 } }">Next</nuxt-link>
      </li>
    </ul>
  </div>
</template>
