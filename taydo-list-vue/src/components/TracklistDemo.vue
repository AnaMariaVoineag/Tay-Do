<script setup>
import { ref, reactive } from "vue"
import taylorImage from "@/assets/images/ts.png"

const basicMessage = ref("It's me, Hi!")
const boundText = ref("Initial Text")

const eventText = ref("Waiting for click...")
const changeText = () => {
  eventText.value = "The text has been changed by the event!"
}

const showConditionalMessage = ref(true)
const toggleCondition = () => {
  showConditionalMessage.value = !showConditionalMessage.value
}

const eras = reactive(["Midnights", "Reputation", "Red", "Fearless"])
</script>

<template>
  <section class="task">
    <h1 class="title">🎵 Basic Level | Tracklist</h1>
    <div>
      <img :src="taylorImage" class="corner-image" />

      <h3>1. Data Display</h3>
      <p>Message: <strong>{{ basicMessage }}</strong></p>

      <h3 class="mt">2. Simple Binding</h3>
      <div class="formLike">
        <input type="text" v-model="boundText" placeholder="Enter text here" />
      </div>
      <p>Entered text: <strong>{{ boundText }}</strong></p>

      <h3 class="mt">3. Events</h3>
      <p>State: <strong>{{ eventText }}</strong></p>
      <button class="accentBtn change-color-btn" @click="changeText">Change Text</button>

      <h3 class="mt">4. Conditionals</h3>
      <button class="accentBtn" @click="toggleCondition">
        Toggle Display (Current state: {{ showConditionalMessage ? "Visible" : "Hidden" }})
      </button>
      <p v-if="showConditionalMessage" class="conditional-msg">
        This message is displayed only if the condition is TRUE!
      </p>

      <h3 class="mt">5. Tracklist</h3>
      <ul class="trackList">
        <li v-for="(era, index) in eras" :key="index">
          {{ index + 1 }}. {{ era }}
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
.task {
  background: var(--card-bg);
  border-radius: 25px;
  padding: 30px;
  box-shadow: var(--shadow);
  position: relative;
}

.title {
  text-align: center;
  margin: 0 0 20px;
  font-size: 22px;
}

.corner-image {
  position: absolute;
  bottom: 0;
  right: 0;
  margin: 0 16px;
  width:280px;
}

@media (max-width: 768px) {
  .corner-image {
    width: 200px;
  }
}

@media (max-width: 480px) {
  .corner-image {
    width: 120px;
  }
}


.formLike input {
  width: 100%;
  height: 50px;
  font: inherit;
  padding: 15px;
  background: var(--input-bg);
  color: var(--text);
  border: 1px solid transparent;
  border-radius: 10px;
  transition: border 0.3s linear;
  margin: 8px 0 10px;
}

.formLike input:focus {
  outline: none;
  border: 1px solid var(--accent);
}

.accentBtn {
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px 12px;
  cursor: pointer;
  transition: background 0.2s ease;
  margin: 6px 0;
}

.accentBtn:hover {
  background: var(--accent-strong);
}

.change-color-btn {
  background: #55b379;
}

.change-color-btn:hover {
  background: #55b379;
}

.trackList {
  list-style: none;
  padding: 0;
  margin: 10px 0 0;
}

.trackList li {
  margin: 6px 0;
}

.mt {
  margin-top: 16px;
}

.conditional-msg {
  margin-top: 8px;
}
</style>
