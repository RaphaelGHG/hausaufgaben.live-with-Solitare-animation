<script setup lang="ts">
import Sidebar from '@/components/sidebarComponent.vue'
import { ref, defineProps, defineEmits } from 'vue'

const  emit  = defineEmits(['reload'])

const props = defineProps({
  headerTitle: {
    type: String,
    required: true
  },
  showButton: {
    type: Boolean,
    required: false,
    default: true
  }
})

const sidebarVisible = ref(false)
const clickCount = ref(0)

function toggleSidebar() {
  sidebarVisible.value = !sidebarVisible.value
}

function reload() {
  toggleSidebar()
  emit('reload')
}

function handleLogoClick() {
  clickCount.value += 1;

  if (clickCount.value === 5) {
    window.location.href = 'src/components/solitare.animation/index_solitare.html';
  }
}
</script>

<template>
  <header class="d-flex justify-content-between align-items-center text-center">
    <div class="p-2 col-sm-2">
      <router-link to="/">
        <img
          src="/src/assets/UntisHomeworkLogo.png"
          alt="logo"
          class="rounded-3 img-fluid"
          width="80"
          style="cursor: pointer;"
          @click="handleLogoClick"
        />
      </router-link>
    </div>
    <div class="p-2 flex-lg-grow-1">
      <h1>{{ props.headerTitle }}</h1>
    </div>
    <div v-if="props.showButton" class="p-2 col-sm-2">
      <button class="btn btn-success btn-lg">
        <router-link to="/new">Hausaufgabe erstellen</router-link>
      </button>
    </div>

    <div class="p-2 me-1">
      <i class="bi bi-list icon" @click="toggleSidebar"></i>
    </div>
  </header>

  <Sidebar
    :visible="sidebarVisible"
    @toggle="toggleSidebar"
    @reload="reload"
  ></Sidebar>
</template>

<style scoped>
header {
  background-color: var(--background-color-secondary);
  color: var(--text-primary-color);

  position: sticky;
  top: 0;

  z-index: 5;
}

.icon {
  cursor: pointer;
  font-size: 250%;
}

a {
  text-decoration: none;
  color: white;
}
</style>
