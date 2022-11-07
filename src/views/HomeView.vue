<script setup lang="ts">
import TheWelcome from "@/components/TheWelcome.vue";
import HelloWorld from "@/components/HelloWorld.vue";
import { ref, markRaw } from 'vue'
import About from "@/components/AboutView.vue";

let activeIndex = ref(0)
let showCom: any = ref(markRaw(TheWelcome))
const changeTab = (i: number) => {
  if (i === activeIndex.value) return
  activeIndex.value = i
  const showList = [TheWelcome, About]
  showCom.value = markRaw(showList[i])
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <a :class="{ 'active': activeIndex === 0 }" @click="changeTab(0)">Home</a>
        <a :class="{ 'active': activeIndex === 1 }" @click="changeTab(1)">About</a>
      </nav>
    </div>
  </header>
  <main>
    <KeepAlive>
      <component :is="showCom"></component>
    </KeepAlive>
  </main>

</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}



nav a:hover {
  background-color: transparent;
  cursor: pointer;
}

nav a.active {
  color: var(--color-text);
  cursor: default;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>