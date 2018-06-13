<template>
  <div class='carousel-view'>

    <div class='carousel-controls__button' @click="previous"></div>
    <transition-group
      class='carousel'
      tag="div">
      <div v-for="(item, index) in slides"
      class='slide'
      :key="index">
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
      // slides: [
      //   {
      //     title: 'I am Slide A',
      //     id: 1
      //   },
      //   {
      //     title: 'I am Slide B',
      //     id: 2
      //   },
      //   {
      //     title: 'I am Slide C',
      //     id: 3
      //   },
      //   {
      //     title: 'I am Slide D',
      //     id: 4
      //   },
      //   {
      //     title: 'I am Slide E',
      //     id: 5
      //   }
      // ]
    }
  },
  created (){
    this.slides = locJSON.CatalogEntryView[0].Images[0].AlternateImages
    //slides.indexOf("item")
  },
  methods: {
    next () {
      const first = this.slides.shift()
      this.slides = this.slides.concat(first)
    },
    previous () {
      const last = this.slides.pop()
      this.slides = [last].concat(this.slides)
    }
  }
}
</script>


<style>
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
.carousel-view {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
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
