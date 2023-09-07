<template>
  <div id="starfield-container">
    <!-- Stars will be generated here -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      stars: [],
    };
  },
  mounted() {
    this.createStars();
    this.animateStars();
  },
  methods: {
    createStars() {
      const numberOfStars = 100;
      const colors = ['#8921C2', '#FE39A4', '#FFFDBB', '#53E8D4', '#25C4F8'];

      for (let i = 0; i < numberOfStars; i++) {
        const star = {
          x: Math.random() * window.innerWidth,
          y: Math.random() * window.innerHeight,
          size: Math.random() * 5 + 1,
          speed: Math.random() * 3 + 2,
          color: colors[Math.floor(Math.random() * colors.length)],
        };
        this.stars.push(star);
      }
    },
    animateStars() {
      const drawStars = () => {
        const container = document.getElementById('starfield-container');
        container.innerHTML = ''; // Clear previous stars

        this.stars.forEach((star) => {
          const starElement = document.createElement('div');
          starElement.className = 'star';
          starElement.style.backgroundColor = star.color;
          starElement.style.width = `${star.size}px`;
          starElement.style.height = `${star.size}px`;
          starElement.style.left = `${star.x}px`;
          starElement.style.top = `${star.y}px`;

          container.appendChild(starElement);

          // Update star position
          star.y += star.speed;
          if (star.y > window.innerHeight) {
            star.y = 0; // Reset to top
          }
        });

        requestAnimationFrame(drawStars);
      };

      drawStars();
    },
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
  border-radius: 50%;
  box-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
  filter: hue-rotate(120deg) blur(2px);
}
</style>
