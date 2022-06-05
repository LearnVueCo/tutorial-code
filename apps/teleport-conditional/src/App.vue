<script setup lang="ts">
import { breakpointsTailwind, useBreakpoints } from '@vueuse/core'

const breakpoints = useBreakpoints(breakpointsTailwind)

const isDesktop = breakpoints.greater('md')
</script>

<template>
  <main>
    <h1>This is my article</h1>
    <p>By Matt Maribojoc</p>
    <div id="toc" />
    <article>
      <section v-for="i in 5">
        <h2 :id="`section-${i}`">Section {{ i }}</h2>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Adipisci
          similique architecto sunt hic incidunt? In, repudiandae? Quo ex
          excepturi ipsam! Similique sint porro maxime optio quos, ducimus
          tempore maiores, eveniet fugit dolorum, natus voluptatum quas totam
          necessitatibus voluptate voluptatem officiis placeat!
        </p>
        <p>
          Officiis eligendi ducimus alias quisquam ad. Ipsum eveniet maiores
          nesciunt ad. Atque, dignissimos fugit porro modi facere consequatur
          tempora repellat explicabo nostrum quasi! Doloribus architecto, earum
          recusandae minus culpa repellat perspiciatis tempora quo vitae
          cupiditate eligendi qui nihil totam odit modi obcaecati est laboriosam
          maxime. Praesentium ex maxime quo. Expedita pariatur quaerat nobis cum
          maxime qui ipsam, vero dicta.
        </p>
      </section>
    </article>
  </main>

  <Teleport to="#toc" :disabled="isDesktop">
    <component :is="isDesktop ? 'aside' : 'div'" class="toc">
      <div>
        <h4>Table of Contents</h4>
        <nav>
          <ul>
            <li v-for="i in 5">
              <a :href="`#section-${i}`">Section {{ i }}</a>
            </li>
          </ul>
        </nav>
      </div>
    </component>
  </Teleport>
</template>

<style>
* {
  font-family: 'Rubik', sans-serif;
}

html {
  background: #ecf0f1;
}

#app {
  width: 80%;
  margin: 0 auto;
  display: flex;
  gap: 4rem;
}

.toc {
  min-width: 200px;
}

aside div {
  position: sticky;
  top: 40px;
}

nav ul {
  list-style-type: none;
  padding: 0;
}

nav ul a {
  color: black;
  text-decoration: none;
}

nav ul a:hover {
  color: #333;
  text-decoration: underline;
}
</style>
