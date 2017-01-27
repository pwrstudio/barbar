<template>
  <div id="app">
    <img src='./assets/face.jpg'>
  </div>
</template>

<script>
import Chance from 'chance'

export default {
  name: 'app',

  mounted () {
    const synth = window.speechSynthesis
    if (!window.speechSynthesis) {
      window.alert('Your browser does not support speech synthesis')
    } else {
      const voices = synth.getVoices()
      const chance = new Chance()
      console.dir(voices)
      // const voiceIndex = chance.integer({min: 0, max: (voices.length - 1)})
      setInterval(() => {
        console.log(voices.length)
        console.dir(voices)
        let sentence = chance.sentence()
        let utterThis = new window.SpeechSynthesisUtterance(sentence + chance.weighted(['', '?'], [5, 1]))
        utterThis.voice = voices[0]
        utterThis.rate = 0.7
        utterThis.pitch = 0.7
        synth.speak(utterThis)
      }, 2000)
    }
  }
}
</script>

<style>

body, html {
  background: #000000;
  overflow: hidden;
  cursor: none;
}

  img {
    display: block;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    height: 300px;
    max-height: 50vh;
    max-width: 50vw;
  }
</style>
