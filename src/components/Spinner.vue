<template>
    <div class="picture-container">
        <div class="spinner"></div>
    </div>
</template>

<script>
    export default {

    }
</script>

<style scoped>
.spinner {
  position: relative;
  height: 100px;
  width: 100px;
  background: linear-gradient(to bottom, rgb(254, 0, 1) 50%, white 50% );
  border-radius: 50%;
  border: 8px solid black;
  animation: spin 1s linear infinite;
  margin: 30px 0 0 40px;
}

.spinner::after {
  content: '';
  position: absolute;
  height: 38px;
  width: 38px;
  border-radius: 50%;
  background: white;
  top: 50px;
  left: 50px;
  transform: translate(-50%, -50%);
  box-shadow: inset 0 0 0 8px black, inset 0 0 0 10px white, inset 0 0 0 12px black;

}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>