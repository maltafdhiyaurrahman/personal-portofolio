<template>
  <nav
    :class="[
      'custom-navbar d-flex align-items-center justify-content-between px-4 py-3',
      navTheme
    ]"
  >
    <!-- Logo -->
    <div class="logo fw-bold">Altaf.</div>

    <!-- Burger Menu (Mobile) -->
    <button
      class="navbar-toggler d-lg-none border-0"
      type="button"
      @click="toggleMenu"
    >
      <i class="bi" :class="isMenuOpen ? 'bi-x-lg' : 'bi-list'"></i>
    </button>

    <!-- Menu + Notif Mobile -->
    <div
      v-if="isMenuOpen && isMobile"
      class="mobile-menu d-flex flex-column align-items-center mt-3 w-100"
    >
      <ul class="nav-menu list-unstyled mb-3 w-100 text-center">
        <li
          v-for="(item, i) in menu"
          :key="i"
          class="my-2"
        >
          <a
            :href="'#' + item.toLowerCase()"
            class="nav-link"
            :class="{ active: activeMenu === item }"
            @click="setActive(item); closeMenu()"
          >
            {{ item }}
          </a>
        </li>
      </ul>

      <!-- Notifikasi di Mobile -->
      <div class="notification-wrapper mt-2">
        <div class="notif-icon position-relative" @click="toggleNotif">
          <i class="bi bi-bell"></i>
          <span
            v-if="hasNewUpdates"
            class="notif-badge position-absolute top-0 start-100 translate-middle rounded-circle"
          ></span>
        </div>

        <div v-if="showNotif" class="notif-dropdown mt-2">
          <p v-if="updates.length === 0" class="mb-0 text-center text-muted">Tidak ada pembaruan</p>
          <ul v-else class="list-unstyled mb-0">
            <li v-for="(update, i) in updates" :key="i">{{ update }}</li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Menu Desktop -->
    <ul
      class="nav-menu list-unstyled mb-0 text-center d-none d-lg-flex flex-lg-row"
    >
      <li
        v-for="(item, i) in menu"
        :key="i"
        class="mx-lg-2"
      >
        <a
          :href="'#' + item.toLowerCase()"
          class="nav-link"
          :class="{ active: activeMenu === item }"
          @click="setActive(item)"
        >
          {{ item }}
        </a>
      </li>
    </ul>

    <!-- 🔔 Notifikasi Desktop -->
    <div class="notification-wrapper d-none d-lg-block position-relative">
      <div class="notif-icon" @click="toggleNotif">
        <i class="bi bi-bell"></i>
        <span
          v-if="hasNewUpdates"
          class="notif-badge position-absolute top-0 start-100 translate-middle rounded-circle"
        ></span>
      </div>

      <div v-if="showNotif" class="notif-dropdown position-absolute end-0 mt-2">
        <p v-if="updates.length === 0" class="mb-0 text-center text-muted">Tidak ada pembaruan</p>
        <ul v-else class="list-unstyled mb-0">
          <li v-for="(update, i) in updates" :key="i">{{ update }}</li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue"

const menu = ["Home", "About", "Projects", "Contact"]
const activeMenu = ref("Home")
const navTheme = ref("dark-theme")
const isMenuOpen = ref(false)
const isMobile = ref(false)
const showNotif = ref(false)
const hasNewUpdates = ref(false) // 🔴 tampilkan badge jika true
let observer = null

// Hardcoded pembaruan
const updates = ref([
  "Belum ada perbaruan",
])

const setActive = (item) => {
  activeMenu.value = item
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  if (isMobile.value) isMenuOpen.value = false
}

const toggleNotif = () => {
  showNotif.value = !showNotif.value
  hasNewUpdates.value = false // badge hilang setelah diklik
}

function observeSections() {
  const options = { threshold: 0.6 }
  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const sectionId = entry.target.getAttribute("id")

        // 🔹 Tema navbar
        const sectionClass = entry.target.classList.contains("dark-section")
          ? "dark-theme"
          : "light-theme"
        navTheme.value = sectionClass

        // 🔹 Menu aktif
        let formattedName = sectionId.charAt(0).toUpperCase() + sectionId.slice(1)
        if (sectionId === "skills") formattedName = "About"
        activeMenu.value = formattedName
      }
    })
  }, options)

  document.querySelectorAll("section").forEach((sec) => observer.observe(sec))
}

onMounted(() => {
  observeSections()
  const handleResize = () => {
    isMobile.value = window.innerWidth < 992
    if (!isMobile.value) isMenuOpen.value = false
  }
  handleResize()
  window.addEventListener("resize", handleResize)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<style scoped>
.custom-navbar {
  background: transparent;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  transition: color 0.3s ease, background 0.3s ease;
}

.logo {
  font-size: 1.5rem;
  transition: color 0.3s ease;
}

.nav-menu {
  border-radius: 50px;
  padding: 6px 20px;
  backdrop-filter: blur(10px);
}
.nav-menu .nav-link {
  font-weight: 500;
  padding: 6px 15px;
  border-radius: 20px;
  transition: all 0.3s ease;
}

/* 🔔 Notifikasi */
.notification-wrapper {
  cursor: pointer;
}
.notif-icon {
  font-size: 1.5rem;
  position: relative;
}
.notif-badge {
  width: 10px;
  height: 10px;
  background: #e74c3c;
  border: 2px solid white;
}
.notif-dropdown {
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.15);
  padding: 10px;
  min-width: 220px;
  z-index: 1001;
}
.notif-dropdown li {
  padding: 6px 0;
  border-bottom: 1px solid #eee;
  font-size: 0.9rem;
}
.notif-dropdown li:last-child {
  border-bottom: none;
}

/* 🌑 Dark theme */
.dark-theme .logo,
.dark-theme .nav-link,
.dark-theme .navbar-toggler,
.dark-theme .notif-icon {
  color: white;
}
.dark-theme .nav-menu {
  background: rgba(255, 255, 255, 0.1);
}
.dark-theme .nav-link.active,
.dark-theme .nav-link:hover {
  background: white;
  color: #303030;
}
.dark-theme .notif-dropdown {
  background: #1e1e1e;
  color: white;
  border: 1px solid #444;
}

/* 🌕 Light theme */
.light-theme .logo,
.light-theme .nav-link,
.light-theme .navbar-toggler,
.light-theme .notif-icon {
  color: #303030;
}
.light-theme .nav-menu {
  background: rgba(0, 0, 0, 0.05);
}
.light-theme .nav-link.active,
.light-theme .nav-link:hover {
  background: #303030;
  color: white;
}
.light-theme .notif-dropdown {
  background: white;
  color: #303030;
}

/* 📱 Mobile */
@media (max-width: 991px) {
  .mobile-menu .nav-menu {
    border-radius: 12px;
    padding: 12px;
    width: 100%;
    text-align: center;
  }
  .mobile-menu .nav-link {
    display: block;
    border-radius: 8px;
    margin: 4px 0;
  }
}
</style>
