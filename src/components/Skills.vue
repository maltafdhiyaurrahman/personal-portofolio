<template>
  <section id="skills" class="skills light-section py-5">
    <div class="container">
      <div class="skills-box mx-auto p-4">
        <!-- Judul -->
        <div class="text-center text-white mb-5">
          <h1 class="fw-bold">Skills</h1>
          <p class="lead mt-2">Some of the newest technology that I use</p>
        </div>

        <!-- Grid Skill -->
        <div class="row g-3 justify-content-center">
          <div
            class="col-6 col-sm-4 col-md-3 col-lg-2"
            v-for="(skill, index) in skills"
            :key="index"
          >
            <div
              class="card h-100 d-flex flex-column align-items-center justify-content-center p-3 skill-card"
            >
              <i
                :class="['fa-2x mb-2', skill.icon, skill.class]"
                :aria-label="skill.name"
              ></i>
              <small class="fw-semibold text-center">{{ skill.name }}</small>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  { name: "Vue.js", icon: "fab fa-vuejs", class: "vue-icon" },
  { name: "Angular", icon: "fab fa-angular", class: "angular-icon" },
  { name: "Bootstrap", icon: "fab fa-bootstrap", class: "bootstrap-icon" },
  { name: "JavaScript", icon: "fab fa-js", class: "js-icon" },
  { name: "HTML5", icon: "fab fa-html5", class: "html-icon" },
  { name: "CSS3", icon: "fab fa-css3-alt", class: "css-icon" },
];
</script>

<style scoped>
.skills {
  background: #fff;
}

.skills-box {
  background: #303030;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  max-width: 95%;
}

.skill-card {
  border-radius: 10px;
  background: #fff;
  color: #303030;
  text-align: center;
  min-height: 110px;
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.skill-card i {
  color: #303030;
  transition: color 0.3s ease;
}

.skill-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
}

/* Warna brand pas hover */
.skill-card:hover .vue-icon {
  color: #42b883;
}
.skill-card:hover .angular-icon {
  color: #dd0031;
}
.skill-card:hover .bootstrap-icon {
  color: #7952b3;
}
.skill-card:hover .js-icon {
  color: #f7df1e;
}
.skill-card:hover .html-icon {
  color: #e34f26;
}
.skill-card:hover .css-icon {
  color: #1572b6;
}
</style>
