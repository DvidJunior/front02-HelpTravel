<template>
  <div class="timeline-item" v-if="isVisible">
    <div :class="['timeline-item-content', { 'active': isActive }]">
      <time :datetime="date">{{ date }}</time>
      <p>{{ content }}</p>
      <span class="circle"></span>
    </div>
  </div>
</template>
  
<script>
import { gsap } from "gsap";

export default {
  props: {
    date: {
      type: String,
      required: true
    },
    content: {
      type: String,
      required: true
    },
    delay: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      isActive: false,
      isVisible: false
    };
  },
  mounted() {
    setTimeout(() => {
      this.isVisible = true;
      this.isActive = true;
    }, this.delay);

    this.isVisible = true;
    gsap.from(this.$el, {
      x: -100,
      opacity: 0,
      delay: this.delay / 1000,  // Convierte milisegundos en segundos para GSAP
      duration: 1.5,
      ease: "elastic.out(1, 0.3)"
    });

  }
};
</script>
  
<style scoped>
  .timeline-item {
    padding: 10px 0;
    position: relative;
  }
  
  .timeline-item-content {
    padding-left: 40px;
    position: relative;
    transition: opacity 1s, transform 1s;
    opacity: 0;
    transform: translateX(-50px);
    opacity: 0;
  }

  .timeline-item-content.active {
  opacity: 1;
  transform: translateX(0);
  }

  .circle {
    width: 20px;
    height: 20px;
    top: 10px;
    left: 0;
    position: absolute;
    background-color: #2f4538 ;
    border-radius: 50%;
  }

</style>