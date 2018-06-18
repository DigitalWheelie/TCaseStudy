<template>
  <div class='carousel-view'>

    <div class='carousel-controls__button' @click="previous"></div>
    <transition-group
      class='carousel'
      tag="div">
      <div v-for="(item, index) in slides"
      class='slide'
      :key="(item.image).split(/[/]+/).pop()">
        <img v-bind:src="item.image" width="50px" height="50px">
      </div>

    </transition-group>
    <div class='carousel-controls__button next' @click="next"></div>

  </div>
</template>


<script>
import locJSON from './assets/item-data.json'
export default {
  data () {
    return {
      slides: null
    }
  },
  created (){
    this.slides = locJSON.CatalogEntryView[0].Images[0].AlternateImages
    //slides.indexOf("item")
  },
  methods: {
    next () {
      const last = this.slides.pop()
      this.slides = [last].concat(this.slides)
    },
    previous () {
      const first = this.slides.shift()
      this.slides = this.slides.concat(first)
    }
  }
}
</script>


<style>
.carousel-view {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 100;
}
.carousel-controls__button{
  background: url('./assets/arrow.png');
  background-repeat: no-repeat;
  background-position: center;
  height: 3em;
  width: 2em;
  cursor: pointer;
}
.carousel-controls__button.next{
  transform: scaleX(-1);
}
.carousel {
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  justify-content: center;

  width: 11em;
}
.slide {
  margin: .25em;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: transform 0.3s ease-in-out;
}
.slide:first-of-type {
  opacity: 0;
}
.slide:last-of-type {
  opacity: 0;
}
</style>
