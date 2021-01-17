<template>
  <span :class="`spin-${align}`">
    <div class="spinner">
      <div class="bounce1" />
      <div class="bounce2" />
      <div class="bounce3" />
    </div>
  </span>
</template>

<script>
export default {
  name: "Spinner",
  props: {
    align: {
      type: String,
      default: "left",
    },
  },
};
</script>

<style scoped>
.spin-left {
  float: left !important;
  display: inline-block;
  text-align: left;  
  padding: 15px 20px;
  font-size: 14px;
  color: #ccc;
  border-radius: 30px;
  line-height: 1.25em;
  font-weight: 100;
  opacity: 0.2;
}
.spin-right {
  float: right !important;
  display: inline-block;
  text-align: right;
  padding: 15px 20px;
  font-size: 14px;
  border-radius: 30px;
  line-height: 1.25em;
  font-weight: 100;
  opacity: 0.2;
}
.spinner {
  margin: 0;
  width: 30px;
  text-align: center;
}
.spinner > div {
  width: 10px;
  height: 10px;
  border-radius: 100%;
  display: inline-block;
  animation: bouncedelay 1.4s infinite ease-in-out both;
  background: rgba(0, 0, 0, 1);
}

.spinner .bounce1 {
  -webkit-animation-delay: -0.32s;
  animation-delay: -0.32s;
}

.spinner .bounce2 {
  -webkit-animation-delay: -0.16s;
  animation-delay: -0.16s;
}

@keyframes bouncedelay {
  0%,
  80%,
  100% {
    -webkit-transform: scale(0);
    transform: scale(0);
  }
  40% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}
</style>