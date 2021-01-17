<template>
  <div :class="aStyle">
    {{ content }}
  </div>
</template>

<script>
export default {
  name: "Avatar",
  props: {
    content: {
      type: String,
      default: "A",
    },
    second: {
      type: Boolean,
      default: false
    },
    align: {
      type: String,
      default: "left",
    },
  },
  data() {
    return {
      aStyle: "avatar"
    }
  },
  created() {
    this.aStyle = this.second ? "avatar second" : "avatar";
    this.aStyle += ` ${this.align}`
  }
}
</script>

<style scoped>
.avatar {
  border-radius: 50%;
  text-align: center;
  font-size: 1rem;
  padding: 0.65rem;
  width: 40px;
  height: 40px;
  background: #C8EDFD;
  color: #1c204e; 
  margin: 0px 8px; 
}
.avatar.second {
  background: #1c204e;
  color: #C8EDFD;
}
.avatar.left {
  float: left !important;
}
.avatar.right {
  float: right !important;
}
</style>