<template>
  <section class="about-me py-5 light-section" id="about">
    <div class="container">
      <div class="row align-items-center">
        <!-- FOTO -->
        <div class="col-12 col-md-5 d-flex justify-content-center mb-4 mb-md-0">
          <div class="image-wrapper">
            <div class="bg-block"></div>
            <img 
              src="@/assets/foto.jpg" 
              alt="Portrait of Muhammad Altaf Dhiyaurrahman" 
              class="profile-img"
              loading="lazy"
            />
          </div>
        </div>

        <!-- TEKS -->
        <div class="col-12 col-md-7 text-center text-md-start">
          <h2 class="text-uppercase text-muted fw-light mb-2 mt-3 section-label">
            About Me ───
          </h2>
          <h3 class="fw-bold mb-4 tight-heading">
            Muhammad <br /> Altaf <br /> Dhiyaurrahman
          </h3>
          <p class="lead mt-4">
            I am a fresh graduate of a Bachelor's degree in Informatics with a GPA of 3.51 and
            bring <strong>1 year experience as Frontend Web Developer</strong>. 
            I specialize in building scalable applications using Vue.js and Angular, always prioritizing clean code and optimal web performance. I am eager to contribute my technical and teamwork skills to an innovative environment.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-me {
  background: #fff;
}

.image-wrapper {
  position: relative;
  display: inline-block;
  width: 100%;
  max-width: 280px;
  aspect-ratio: 4/5; /* biar proporsi tetap konsisten */
}

.bg-block {
  position: absolute;
  top: 20px;
  left: 20px;
  width: 100%;
  height: 100%;
  background: #303030;
  border-radius: 25px;
  z-index: 1;
}

.profile-img {
  position: relative;
  z-index: 2;
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 25px;
}

/* Heading Nama */
.tight-heading {
  line-height: 0.95;
  text-transform: uppercase;
  font-size: clamp(1.8rem, 5vw, 3rem);
  letter-spacing: 1px;
}

.section-label {
  font-size: clamp(0.75rem, 1.5vw, 0.9rem);
  letter-spacing: 2px;
}

/* Paragraf */
.lead {
  font-size: clamp(0.95rem, 2vw, 1.1rem);
}
</style>
