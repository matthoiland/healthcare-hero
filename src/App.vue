<template>
  <div id="app" v-bind:class="{dark: (slide ===6)}">

    <!-- Welcome -->
    <transition name="slide-move">
      <div class="slide" v-if="slide === 1">
        <h1>Find your healthcare superhero</h1>
        <h3>name</h3>
        <div class="buttons">
          <button v-on:click="changeSlide(2)">Let's Do This!</button>
        </div>
        <h5>A <strong>Healthsparq Labs</strong> Project</h5>
      </div>
    </transition>

    <!-- Gender -->
    <transition name="slide-move">
      <div class="slide" v-if="slide === 2">
        <h1>My superhero's gender would be...</h1>
        <div class="buttons">
          <button v-on:click="changeSlide(3), gender='female'">Female</button>
          <button v-on:click="changeSlide(3), gender='male'">Male</button>
          <button v-on:click="changeSlide(3), gender='neutral'">Neutral</button>
        </div>
        <h5>A <strong>Healthsparq Labs</strong> Project</h5>
      </div>
    </transition>

    <!-- Empathize with -->
    <transition name="slide-move">
      <div class="slide" v-if="slide === 3">
        <h1>I would most closely associate with...</h1>
        <div class="buttons">
          <button v-on:click="changeSlide(4), associate='doctor_provider'">Medical Professional</button>
          <button v-on:click="changeSlide(4), associate='patient_power'">Patient Power</button>
          <button v-on:click="changeSlide(4), associate='health_tech'">Health Technology</button>
          <button v-on:click="changeSlide(4), associate='paper_pusher'">Policy Expert</button>
        </div>
        <h5>A <strong>Healthsparq Labs</strong> Project</h5>
      </div>
    </transition>

    <!-- Hate -->
    <transition name="slide-move">
      <div class="slide" v-if="slide === 4">
        <h1>What drives me crazy about healthcare is...</h1>
        <div class="buttons">
          <button v-on:click="changeSlide(5), hate='wait_times'">Long Wait Times</button>
          <button v-on:click="changeSlide(5), hate='paperwork'">Paperwork</button>
          <button v-on:click="changeSlide(5), hate='costs'">Crazy Costs</button>
          <button v-on:click="changeSlide(5), hate='on_fire'">Being On Fire</button>
        </div>
        <h5>A <strong>Healthsparq Labs</strong> Project</h5>
      </div>
    </transition>

    <!-- Animal -->
    <transition name="slide-move">
      <div class="slide" v-if="slide === 5">
        <h1>My spirit animal is most similar to a...</h1>
        <div class="buttons">
          <button v-on:click="changeSlide(6), animal='manatee'">Manatee</button>
          <button v-on:click="changeSlide(6), animal='elephant'">Elephant</button>
          <button v-on:click="changeSlide(6), animal='horse'">Tiny Horse</button>
          <button v-on:click="changeSlide(6), animal='raptor'">Velociraptor</button>
        </div>
        <h5>A <strong>Healthsparq Labs</strong> Project</h5>
      </div>
    </transition>

    <!-- Result -->
    <transition name="slide-move">
      <div class="slide" v-if="slide === 6">
        <h3 class="left">You are</h3>
        <h1>{{your_name}}</h1>
        <div class="buttons">
          <button v-on:click="changeSlide(2)">Start Over</button>
        </div>
        <h5>A <strong>Healthsparq Labs</strong> Project</h5>
      </div>
    </transition>
  </div>
</template>

<script>
import Names from './names.js'

export default {
  name: 'app',
  data() {
    return {
      slide: 1,
      gender: null,
      associate: null,
      hate: null,
      animal: null
    }
  },
  computed: {
    your_name() {
      if (!this.gender || !this.associate || !this.hate || !this.animal) {
        return 'The Waitroom Warrior';
      } else {
        return Names[this.gender][this.associate][this.hate][this.animal];
      }
    }
  },
  methods: {
    changeSlide(slide) {
      this.slide = slide;
    }
  }
}
</script>

<style>
  html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    overflow: hidden;
  }
  body {
    font-family: 'Open Sans', sans-serif;
  }
  h1 {
    font-size: 1.7rem;
    font-family: 'Alfa Slab One', cursive;
    font-weight: normal;
    text-transform: uppercase;
    margin: 0;
  }
  @media only screen and (max-width: 500px) {
    h1 { font-size: 1.3rem; }
  }
  h3 {
    font-size: 1rem;
    font-family: 'Gloria Hallelujah', cursive;
    font-weight: normal;
    margin: 0 0 0 150px;
  }
  h3.left {
    margin: 0 0 0 -150px;
  }
  h5 {
    text-align: center;
    font-size: 0.7rem;
    font-weight: normal;
    margin: 0;
  }

  #app {
    width: 100%;
    height: 100%;
    transition: all 500ms ease;
  }

  .slide {
    position: absolute;
    top: 50%; left: 50%;
    transform: translateX(-50%) translateY(-50%);
    text-align: center;
    width: calc(100% - 100px);
    max-width: 360px;
    padding: 40px;
    background: #ffffff;
    box-shadow: 0 4px 20px rgba(0,0,0,0.2);
    border-radius: 6px;
  }

  .slide-move-enter-active { transition: all 500ms cubic-bezier(0.215, 0.610, 0.355, 1.000); }
  .slide-move-leave-active { transition: all 500ms cubic-bezier(0.215, 0.610, 0.355, 1.000); }
  .slide-move-enter {
    opacity: 0;
    transform: translateX(200%) translateY(-50%) !important;
  }
  .slide-move-enter-to {
    opacity: 1;
    transform: translateX(-50%) translateY(-50%) !important;
  }
  .slide-move-leave {
    opacity: 1;
    transform: translateX(-50%) translateY(-50%) !important;
  }
  .slide-move-leave-to {
    opacity: 0;
    transform: translateX(-200%) translateY(-50%) !important;
  }

  .buttons {
    padding: 30px 0;
  }
  button {
    appearance: none;
    width: 100%;
    background: white;
    border: 1px solid #ccc;
    cursor: pointer;
    padding: 14px;
    font-size: 1rem;
    margin: 6px 0;
    outline: none;
  }
  button:hover {
    border-color: #555;
  }

  #app.dark {
    background: #222;
  }
  #app.dark .slide {
    background: #222 !important;
    color: #eee;
    box-shadow: none;
  }
  #app.dark button {
    background: none;
    color: #eee;
    border-color: #555;
  }
  #app.dark button:hover {
    border-color: #999;
  }
</style>
