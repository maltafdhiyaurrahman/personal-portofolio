<template>
  <section id="projects" class="projects py-5 dark-section">
    <div class="container">
      <div class="d-flex justify-content-between align-items-center mb-5">
        <div>
          <h2 class="fw-bold text-white">PROJECTS</h2>
          <p class="lead text-white-50">My Recent Works</p>
        </div>
        <a href="/projects" class="btn custom-btn" v-if="projects.length > 3">See More</a>
      </div>

      <div class="row g-4 justify-content-center">
        <div
          class="col-12 col-sm-6 col-md-4"
          v-for="(project, index) in limitedProjects"
          :key="index"
        >
          <!-- <div
            class="project-card position-relative"
            data-bs-toggle="modal"
            data-bs-target="#projectModal"
            @click="setActiveProject(project)"
          > -->
          <div
            class="project-card position-relative disabled"
          >
            <img :src="project.images[0]" alt="Project Thumbnail" />
            <div class="overlay position-absolute top-0 start-0 h-100 w-100">
              <h5 class="text-white fw-bold">{{ project.title }}</h5>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- <div
      class="modal fade"
      id="projectModal"
      tabindex="-1"
      aria-labelledby="projectModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-lg">
        <div class="modal-content text-white bg-dark">
          <div class="modal-header border-0">
            <h5 class="modal-title fw-bold" id="projectModalLabel">
              {{ activeProject.title }}
            </h5>
            <button
              type="button"
              class="btn-close btn-close-white"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <div id="projectCarousel" class="carousel slide">
              <div class="carousel-indicators">
                <button
                  v-for="(image, index) in activeProject.images"
                  :key="index"
                  type="button"
                  :data-bs-target="'#projectCarousel'"
                  :data-bs-slide-to="index"
                  :class="{ 'active': index === 0 }"
                  :aria-current="index === 0 ? 'true' : null"
                  :aria-label="'Slide ' + (index + 1)"
                ></button>
              </div>
              <div class="carousel-inner rounded mb-4">
                <div
                  v-for="(image, index) in activeProject.images"
                  :key="index"
                  :class="['carousel-item', { 'active': index === 0 }]"
                >
                  <img :src="image" class="d-block w-100 modal-image" alt="..." />
                </div>
              </div>
              <button
                class="carousel-control-prev"
                type="button"
                data-bs-target="#projectCarousel"
                data-bs-slide="prev"
              >
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
              </button>
              <button
                class="carousel-control-next"
                type="button"
                data-bs-target="#projectCarousel"
                data-bs-slide="next"
              >
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
              </button>
            </div>
            
            <p>{{ activeProject.description }}</p>
            <h6 class="fw-bold mt-4">Tech Stack:</h6>
            <ul class="d-flex flex-wrap gap-2 mb-3 list-unstyled">
              <li
                v-for="(tech, i) in techStack"
                :key="i"
                class="list-group-item bg-secondary text-white rounded-pill border-0 px-3 py-1"
              >
                {{ tech }}
              </li>
            </ul>

            <div class="d-flex gap-2 mt-4 justify-content-end">
              <a
                v-if="activeProject.title !== 'Personal Portfolio Website'"
                :href="activeProject.demo"
                target="_blank"
                class="btn btn-solid-primary"
              >
                Live Demo
              </a>
              <a
                :href="activeProject.repo"
                target="_blank"
                class="btn custom-btn"
              >
                Repository
              </a>
            </div>
          </div>
        </div>
      </div>
    </div> -->
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import soon from "@/assets/soon.png";

const projects = [
  {
    title: "coming soon",
    images: [soon], 
    description: "A personal website to showcase my web development projects and skills. Built from scratch with a focus on modern and clean UI/UX.",
    tech: "Vue.js, Bootstrap 5, Vite, JavaScript",
    demo: "#",
    repo: "#",
  },
  {
    title: "coming soon",
    images: [soon], 
    description: "A personal website to showcase my web development projects and skills. Built from scratch with a focus on modern and clean UI/UX.",
    tech: "Vue.js, Bootstrap 5, Vite, JavaScript",
    demo: "#",
    repo: "#",
  },
  {
    title: "coming soon",
    images: [soon], 
    description: "A personal website to showcase my web development projects and skills. Built from scratch with a focus on modern and clean UI/UX.",
    tech: "Vue.js, Bootstrap 5, Vite, JavaScript",
    demo: "#",
    repo: "#",
  },
];

const limitedProjects = computed(() => projects.slice(0, 3));
const activeProject = ref({});

const techStack = computed(() => {
  if (activeProject.value.tech) {
    return activeProject.value.tech.split(",").map((item) => item.trim());
  }
  return [];
});

function setActiveProject(project) {
  activeProject.value = project;
}
</script>

<style scoped>
.carousel-item img {
  aspect-ratio: 16 / 9;
  object-fit: cover;
}
.modal-image {
  width: 100%;
}
.projects {
  background: #303030;
}
.project-card {
  aspect-ratio: 3 / 4;
  border-radius: 15px;
  cursor: pointer;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.project-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
.project-card:hover {
  transform: scale(1.05);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.4);
}
.project-card .overlay {
  background: rgba(0, 0, 0, 0.6);
  opacity: 0;
  transition: opacity 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}
.project-card:hover .overlay {
  opacity: 1;
}
.custom-btn {
  background: transparent;
  background-color: rgba(255, 255, 255, 0.1);
  color: #fff;
  border-radius: 50px;
  backdrop-filter: blur(10px);
}
.custom-btn:hover {
  background-color: #fff;
  color: #303030;
}
.modal-content {
  background: #212121 !important;
}
.modal-title {
  color: #fff;
}
.modal-body {
  padding-top: 1rem;
  overflow-y: auto;
  max-height: 70vh;
}

.btn-solid-primary {
  background-color: white;
  color: #303030;
  border: 1px solid white;
  border-radius: 50px;
  padding: 0.375rem 1.5rem; 
  transition: all 0.3s ease;
}
.btn-solid-primary:hover {
  background-color: transparent;
  background-color: #505050;
  color: white;
}
</style>