<template>
  <section class="contact-section py-5 light-section" id="contact">
    <div class="container">
      <div class="text-center mb-5">
        <h6 class="text-uppercase text-muted fw-light">Contact</h6>
        <h1 class="fw-bold display-2">Let's Collaborate</h1>
      </div>

      <div class="row">
        <div class="col-md-6 d-flex flex-column justify-content-between">
          <div>
            <h5 class="fw-bold mb-4">Get in Touch</h5>
            <p class="mb-3">
              <i class="bi bi-envelope-fill me-2 fs-4"></i>
              altafff02@gmail.com
            </p>
            <p class="mb-3">
              <i class="bi bi-geo-alt-fill me-2 fs-4"></i>
              Bandung, Indonesia
            </p>
          </div>

          <div class="mt-5">
            <h5 class="fw-bold mb-3">Find Me</h5>
            <div class="d-flex gap-3">
              <a href="https://github.com/maltafdhiyaurrahman" target="_blank" rel="noopener noreferrer" class="text-dark fs-4" aria-label="GitHub"><i class="bi bi-github"></i></a>
              <a href="www.linkedin.com/in/muhammad-altaf-dhiyaurrahman" target="_blank" rel="noopener noreferrer" class="text-dark fs-4" aria-label="LinkedIn"><i class="bi bi-linkedin"></i></a>
              <a href="https://www.instagram.com/altafd_/" target="_blank" rel="noopener noreferrer" class="text-dark fs-4" aria-label="Instagram"><i class="bi bi-instagram"></i></a>
              <a href="https://wa.me/6281804021183" target="_blank" rel="noopener noreferrer" class="text-dark fs-4" aria-label="WhatsApp"><i class="bi bi-whatsapp"></i></a>
            </div>
          </div>
        </div>

        <div class="col-md-6">
          <h3 class="fw-bold mb-4">Say Hello</h3>
          <form @submit="handleSubmit"
          >
            <div class="mb-3">
              <input type="text" class="form-control border-0 border-bottom rounded-0" placeholder="Your Name" id="name" name="name" required />
            </div>
            <div class="mb-3">
              <input type="email" class="form-control border-0 border-bottom rounded-0" placeholder="Your Email" id="email" name="email" required />
            </div>
            <div class="mb-3">
              <textarea rows="4" class="form-control border-0 border-bottom rounded-0" placeholder="Your Message" id="message" name="message" row="5" required></textarea>
            </div>
            <div class="text-end">
              <input type="text" name="_gotcha" style="display:none">
              <button type="submit" class="btn btn-custom px-4">Send</button>
              <p v-if="status" :class="{'text-success': isSuccess, 'text-danger': !isSuccess}" class="mt-2 fw-bold">{{ status }}</p>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

const status = ref("");
const isSuccess = ref(false);

function handleSubmit(e) {
  e.preventDefault();
  const data = new FormData(e.target);

  fetch("https://formspree.io/f/xblzryrr", {
    method: "POST",
    body: data,
    headers: { Accept: "application/json" },
  })
    .then((response) => {
      if (response.ok) {
        status.value = "Thanks! Your message has been sent.";
        isSuccess.value = true;
        e.target.reset();
      } else {
        status.value = "Oops! There was a problem.";
        isSuccess.value = false; 
      }
    })
    .catch(() => {
      status.value = "Oops! There was a problem.";
      isSuccess.value = false;
    });
}
</script>

<style scoped>
.contact-section {
  font-family: 'Poppins', sans-serif;
}

.col-md-6 {
  margin-bottom: 2rem;
}
@media(min-width: 768px) {
  .col-md-6 {
    margin-bottom: 0;
  }
}

.form-control {
  box-shadow: none !important;
  font-family: inherit;
  border-radius: 0;
  border-bottom: 2px solid #ccc;
  transition: border-color 0.3s ease;
}
.form-control:focus {
  border-color: #303030;
  box-shadow: none;
}

textarea.form-control {
  min-height: 120px;
}

.btn-custom {
  background-color: #303030;
  color: #fff;
  border-radius: 50px;
  transition: background 0.3s ease;
}
.btn-custom:hover {
  background-color: #505050;
  color: #fff;
}

.d-flex a {
  transition: color 0.3s ease;
}
.d-flex a:hover {
  color: #303030;
}
</style>

