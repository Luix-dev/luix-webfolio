<template>
  <div id="starfield-container">
    <!-- Content other than the stars -->
  </div>
</template>

<script>
export default {
  mounted() {
    const container = document.getElementById('starfield-container');
    const numberOfStars = 100;
    const colors = ['#8921C2', '#FE39A4', '#FFFDBB', '#53E8D4', '#25C4F8'];

    for (let i = 0; i < numberOfStars; i++) {
      const star = document.createElement('div');
      star.className = 'star';

      // Randomly assign color from the global colors
      const color = colors[Math.floor(Math.random() * colors.length)];
      star.style.backgroundColor = color;

      // Randomly assign size
      const size = Math.random() * 5 + 1; // Increased size range
      star.style.width = `${size}px`;
      star.style.height = `${size}px`;

      // Randomly assign position
      star.style.left = `${Math.random() * 100}vw`;
      star.style.top = `${Math.random() * 100}vh`;

      // Randomly assign animation duration
      const speed = Math.random() * 3 + 2;
      star.style.animationDuration = `${speed}s`;

      // Randomly assign hue and glow
      const hue = Math.random();
      const glow = Math.random() * 3;
      star.style.setProperty('--hue', hue);
      star.style.setProperty('--glow', glow);

      container.appendChild(star);
    }
  },
};
</script>

<style>
#starfield-container {
  background-color: black;
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.star {
  position: absolute;
  opacity: 0.8;
  animation: moveStar linear infinite;
  border-radius: 50%;
  filter: brightness(150%) hue-rotate(calc(360deg * var(--hue))) blur(2px);
  box-shadow: 0 0 calc(5px + var(--glow) * 2px) rgba(255, 255, 255, 0.7);
}

@keyframes moveStar {
  from {
    transform: translateY(0px);
  }
  to {
    transform: translateY(100vh);
  }
}
</style>
