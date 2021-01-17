<template>
  <div class="wrapper">
    <div class="chat">
      <div class="chat-container">
        <div class="chat-listcontainer">
          <ul class="chat-message-list">
            <li v-for="(frase, index) in frases" :key="`${index}`">
              <!-- <component v-bind:is="currentComponent"></component> -->

              <Spinner
                v-if="!frase.show"
                :position="isEven(index) ? 'left' : 'right'"
              />
              <div
                v-if="frase.show"
                :class="isEven(index) ? 'message-left' : 'message-right'"
              >
                <div class="message-text">
                  <span v-if="isEven(index)">{{ getQuestion(frase) }}</span>
                  <ul v-else class="options">
                    <li v-for="(option, idx) in frase.options" :key="`${idx}`">
                      {{ option }}
                    </li>
                  </ul>
                </div>
                <div class="message-time">{{ getTime() }}</div>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Spinner from "@/components/Spinner.vue";

export default {
  name: "Chat",
  components: {
    Spinner,
  },
  data() {
    return {
      frases: [
        {
          show: false,
          question: "Hello! Please choose from one of the options below",
          options: ["Option A", "Option B", "Option C"],
          answer: null,
        },
      ],
      log: [],
    };
  },
  mounted() {
    //this.frases.forEach((frase, idx) => this.delayedShow(frase, idx))
    this.delayedShow(this.frases[0]);
    setTimeout(() => {
      this.frases.push({
        show: false,
        question: "Hello! Please choose from one of the options below",
        options: ["Option A", "Option B", "Option C"],
        answer: null,
      });
      this.delayedShow(this.frases[1]);
    }, 2500);
  },
  methods: {
    isEven(value) {
      return value % 2 == 0 ? true : false;
    },
    delayedShow(frase, idx) {
      const mult = idx || 1;
      let delay = 2500 * mult;
      if (!frase.show) {
        setTimeout(() => {
          frase.show = true;
        }, delay);
      }
    },
    getQuestion(frase) {
      return frase.question;
    },
    getTime() {
      return new Date().toLocaleTimeString();
    },
  },
};
</script>

<style scoped>
.wrapper {
  width: 800px;
  margin: 58px auto;
  display: block;
}
@media only screen and (max-width: 800px) {
  .wrapper {
    width: 100%;
    padding: 5px;
  }
  .message-right .message-text ul {
    width: 80%;
  }
}
.chat {
  width: 100%;
  border-radius: 10px;
  padding: 20px;
  background-color: #f7f8f9;
}
.chat-container {
  height: 400px;
  overflow-y: scroll;
  padding-right: 16px;
}

ul {
  margin: 0px;
  padding: 0px;
  list-style: none;
}

.message-left,
.message-right {
  color: #032a43;
}

.message-left {
  text-align: left;
  margin-bottom: 16px;
}
.message-left .message-time {
  display: block;
  font-size: 12px;
  text-align: left;
  padding-left: 15px;
  padding-top: 4px;
  font-family: Courier;
}

.message-left .message-text {
  max-width: 80%;
  display: inline-block;
  background: #edf0f2;
  padding: 15px;
  font-size: 14px;
  border-radius: 30px;
  line-height: 1.5em;
  border-radius: 0px 6px 6px 6px;
}
.message-right {
  text-align: right;
  margin-bottom: 16px;
}
.message-right .message-time {
  display: block;
  font-size: 12px;
  text-align: right;
  padding-right: 15px;
  padding-top: 4px;
  font-family: Courier;
}
.message-right .message-text {
  max-width: 80%;
  line-height: 1.5em;
  display: inline-block;
  background: white;
  padding: 15px;
  font-size: 14px;
  border-radius: 30px;
  line-height: 1.5em;
  text-align: left;
  border-radius: 6px 0px 6px 6px;
}
.message-right .message-text ul {
  width: 400px;
}
</style>