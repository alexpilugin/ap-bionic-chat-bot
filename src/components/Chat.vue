<template>
  <div class="wrapper">
    <div class="chat">
      <div class="chat-container">
        <div class="chat-listcontainer">
          <ul class="chat-message-list">
            <li v-for="(frase, index) in frases" :key="`${index}`">
              <Spinner v-if="!frase.show" align="left" />
              
              <!-- BOT -->
              <Avatar v-if="frase.show" content="m" align="left" />
              <div v-if="frase.show" class="message-left">
                <div class="message-text">
                  <span v-html="getQuestion(frase)"></span>
                </div>
                <div class="message-time">{{ frase.time }}</div>
              </div>

              <!-- USER -->
              <Avatar v-if="frase.show && frase.options" content="Me" align="right" second />
              <div v-if="frase.show && frase.options" class="message-right">
                <div class="message-text">
                  <Radios
                    :id="frase.id"
                    :options="frase.options"
                    :disabled="!!frase.answer"
                    :defaultValue="frase.answer"
                    @change="updateAnswer"
                    inputClass="options"
                  />
                </div>
                <div class="message-time">{{ frase.time }}</div>
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
import Avatar from "@/components/Avatar.vue";
import Radios from "@/components/Radios.vue";
import Spinner from "@/components/Spinner.vue";

export default {
  name: "Chat",
  components: {
    Avatar,
    Radios,
    Spinner,
  },
  data() {
    return {
      frases: [
        {
          id: "q0",
          show: false,
          question: "Hello! Please choose from one of the options below",
          options: ["Option A", "Option B", "Option C"],
          time: this.currentTime(),
          answer: null,
        },
      ],
      log: [],
    };
  },
  mounted() {
    //this.frases.forEach((frase, idx) => this.delayedShow(frase, idx))
    this.delayedShow(this.frases[0]);
  },
  methods: {
    currentTime: () => new Date().toLocaleTimeString(),
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
    updateAnswer(answer) {
      this.frases.find((item) => item.id === answer.id).answer = answer.value;
      this.log.push(answer.value); // log
      const counter = this.frases.length + 1;

      if (answer.value !== "No") {       
        this.frases.push({
          id: `q${counter}`,
          show: false,
          question: `<b>${answer.value}</b>? Great choice! Do you want to continue?`,
          options: ["Yes", "No"],
          time: this.currentTime(),
          answer: null,
        });              
      } else {
        this.frases.push({
          id: `q${counter}`,
          show: false,
          question: `<b>${answer.value}</b>? Good Bye!`,
          options: null,
          time: this.currentTime(),
          answer: null,
        }); 
      }
      this.delayedShow(this.frases[this.frases.length - 1]);
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
    width: 70%;
  }
}
.chat {
  width: 100%;
  border-radius: 10px;
  padding: 20px;
  background-color: #f7f8f9;
}
.chat-container {
  height: 500px;
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
  max-width: 70%;
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
  max-width: 70%;
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