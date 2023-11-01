<template>
    <div class="timeline">
      <slot></slot>
    </div>
</template>
  
  <script>
  export default {
    name: "Timeline"
  };
  </script>
  
<style scoped >
.timeline {
    position: relative;
    max-width: 600px;
    margin: 0 auto;
  }

</style>