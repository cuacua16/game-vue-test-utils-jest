<template>
    <div class="options-container">
        <ul>
            <li
                v-for="(option, i) in options"
                :key="i"
                :style="
                    option.correct ? 'background-color: #00ff00;' : 
                    option.correct === false ? 'background-color: #ff0000;' : ''"
            >
                <button style="border:none; background-color: inherit; color:inherit; font-size: inherit;" :disabled="disabled || option.disabled" @click="$emit('selected', option)">
                    <span v-if="option.name">{{ option.name }}</span>
                    <div v-else class="spinner"></div>
                </button>

            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        options: Array,
        disabled: Boolean
    },
    data() {
        return {

        }
    },

}
</script>

<style scoped>
.spinner {
  /* position: absolute;
  top: 50%;
  left: 50%; */
  transform: translate(-50%, -50%);
  height: 16px;
  width: 16px;
  box-sizing: border-box;
  background: conic-gradient(
    from 90deg at 50% 50%,
    rgba(39, 174, 96, 0) 0deg,
    rgba(31, 144, 255, 0) 0.04deg,
    #1f90ff 360deg
  );
  border-radius: 16px;
  /* previous code */
  animation: 1s rotate infinite linear;
}
.spinner::before {
  content: "";
  /* position: absolute;
  left: 50%;
  top: 50%; */
  transform: translate(-50%, -50%);
  height: 12px;
  width: 12px;
  background: #fff;
  border-radius: 28px;
}
.spinner::after {
  content: "";
  /* position: absolute;
  right: 0;
  top: 50%; */
  transform: translateY(-50%);
  height: 8px;
  width: 8px;
  background: #1f90ff;
  border-radius: 8px;
}
@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>