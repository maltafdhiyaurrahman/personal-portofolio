<template>
  <section class="hero text-white position-relative dark-section" id="home">
    <div class="container d-flex flex-column justify-content-center align-items-center min-vh-100 text-center">
      <h2 class="text-uppercase fw-light mb-2">Hi, I am Altaf</h2>
      <h1 class="display-3 fw-bold line-tight">Frontend Web</h1>
      <h1 class="display-3 fw-bold line-tight text-shadow mb-4">Developer</h1>
      <p class="text-white mt-4">
        Transforming the design system into a highly performant and user-centric web product. 
      </p>
    </div>

    <div class="scroll-box"></div>

    <div class="scroll-down-wrapper">
      <svg width="150" height="150" viewBox="0 0 100 100">
        <defs>
          <path id="circlePath" d="M50,50 m-35,0 a35,35 0 1,1 70,0 a35,35 0 1,1 -70,0" />
        </defs>

        <circle cx="50" cy="50" r="50" fill="white" />

        <g class="rotate-text">
          <text font-size="10" fill="#303030" letter-spacing="2" text-transform="uppercase">
            <textPath href="#circlePath" startOffset="0%">
              --------- SCROLL DOWN --------- SCROLL DOWN 
            </textPath>
          </text>
        </g>

        <circle cx="50" cy="50" r="30" fill="#303030" />

        <text
          x="50%"
          y="54%"
          text-anchor="middle"
          font-size="50"
          fill="white"
          dominant-baseline="middle"
        >
          &#8595;
        </text>
      </svg>
    </div>
  </section>
</template>

<style scoped>
.hero {
  width: 100%;
  background-color: #303030;
  position: relative;
  overflow: hidden;
}

.line-tight {
  margin-bottom: 0;
  line-height: 0.55;
  font-size: 8rem;
}

.text-shadow {
  text-shadow: 0 -4px 15px rgba(0, 0, 0, 0.8);
}

.scroll-box {
  position: absolute;
  bottom: 0px;
  left: 0;
  right: 0;
  height: 40px;
  background: white;
  box-shadow: 0 0 10px rgba(0,0,0,0.05);
  z-index: 1;
}

.scroll-down-wrapper {
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  width: 12vw;  
  max-width: 120px; 
  min-width: 65px;  
  aspect-ratio: 1/1; 
  z-index: 10;
}

.scroll-down-wrapper svg {
  width: 100%;
  height: 100%;
}

.rotate-text {
  animation: rotateText 10s linear infinite;
  transform-origin: 50% 50%;
}
  
.rotate-text text {
  letter-spacing: 0;
}

@keyframes rotateText {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}


@media (max-width: 992px) { 
  .line-tight {
    font-size: 5rem;
    line-height: 0.7;
  }

  .scroll-down-wrapper {
    width: 120px;
    height: 120px;
  }

  .scroll-box {
    height: 70px;
  }
}

@media (max-width: 576px) { 
  .line-tight {
    font-size: 2.8rem;
    line-height: 0.9;
  }

  h2 {
    font-size: 1rem;
  }

  p {
    font-size: 0.85rem;
    max-width: 90%;
  }

  .scroll-down-wrapper {
    width: 90px;
    height: 90px;
  }

  .scroll-box {
    height: 60px;
  }
}
</style>
