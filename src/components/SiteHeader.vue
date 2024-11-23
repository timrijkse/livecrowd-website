<script setup lang="ts">
import { onMounted, ref } from 'vue'
import Logo from './shared/Logo.vue'
import IconHamburger from './icons/IconHamburger.vue'
import ButtonHelp from './shared/ButtonHelp.vue'

const navigationItems = ref([
  { label: 'Home', href: '#' },
  { label: 'How we work', href: '#' },
  { label: 'What we do', href: '#' },
])

const isOpen = ref(false)
const headerHeight = ref(0)
const headerNav = ref(null)
const paddingBottom = ref(32)

// get header nav element
onMounted(() => {
  headerNav.value = document.querySelector('.header-nav')
})

const toggleOpen = () => {
  isOpen.value = !isOpen.value

  if (isOpen.value) {
    headerHeight.value =
      headerNav.value?.clientHeight + headerNav.value?.offsetTop + paddingBottom.value || 0
  } else {
    headerHeight.value = 0
  }
}
</script>

<template>
  <header class="header" :class="{ open: isOpen }">
    <div class="background" :style="{ height: headerHeight + 'px' }"></div>
    <div class="header-content">
      <Logo />
      <IconHamburger :is-open="isOpen" @click="toggleOpen" class="header-hamburger" />
      <ButtonHelp class="header-button-help" />
    </div>

    <nav class="header-nav">
      <ul>
        <li v-for="(item, index) in navigationItems" :key="item.label">
          <a @click="toggleOpen" :href="item.href" :style="{ transitionDelay: `${index * 0.2}s` }">
            <span>{{ item.label }}</span>
          </a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
.header {
  position: relative;
  width: 100vw;
  max-width: var(--site-width);
  margin: 0 auto;
  z-index: 100;
}

.background {
  transition:
    height 0.3s ease-in-out,
    box-shadow 0.3s ease-in-out;
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 0;
  background-color: #fff;
  box-shadow: 0px 4px 54px rgba(0, 0, 0, 0);
  transition-delay: 0.15s;
}

.open .background {
  height: 100%;
  box-shadow: 0px 4px 54px rgba(0, 0, 0, 0.25);
  transition-delay: 0s;
}

.header-hamburger {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.header-button-help {
  position: absolute;
  right: -60px;
}

.header-content {
  position: relative;
  display: flex;
  overflow: hidden;
  align-items: center;
  justify-content: space-between;
  width: 100vw;
  padding: 16px var(--site-padding);
  z-index: 2;
}

.header-nav {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 2;
  width: 100%;
  text-align: center;
}

.header-nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.header-nav li {
  margin-bottom: 8px;
}

.header-nav a {
  overflow: hidden;
  display: block;
  text-decoration: none;
  color: #000;
}

.header-nav a span {
  display: inline-block;
  transition: transform 0.3s ease-in-out;
  transform: translateY(-100%);
  font-size: 16px;
  line-height: 1.2;
}

.open .header-nav a span {
  transform: translateY(0);
}
</style>
