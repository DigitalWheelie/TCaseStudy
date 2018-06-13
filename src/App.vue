<template>
  <div class="appWrapper">
    <div id="app">
      <div class="prodMain">
      <h1>{{ csTitle }}</h1>
      <div id="primaryImage">
         <img v-bind:src="csPImage" width="400px" height="400px">
       </div>

       <carousel></carousel>

    </div>

    <div class="prodDetails">
      <div class="price"><span class="priceValue">{{ csPrice }}</span> <span class="priceQualifier">{{ csPriceQualifier }}</span></div>
      <div>
        <img src="./assets/mock2a.png">
      </div>

      <div id="purchase" class="purchaseWrapper">
        <span v-if="availOnline"><img src="./assets/btnOnline.png"></span>
        <span v-if="availInstore"><img src="./assets/btnPickUp.png"></span>
      </div>

      <div>
        <img src="./assets/mock2b.png">
      </div>
    </div>

    <div class="prodRatings">
      <div>
        <img src="./assets/mock3.png">
      </div>
    </div>

    </div>
  </div>
</template>



<script>
  import Carousel from './Carousel.vue';
  import locJSON from './assets/item-data.json'

  // import axios from 'axios'
  export default {
    name: 'App',
    components: {
      'carousel': Carousel
    },
    data () {
      return {
        csTitle: null,
        csAImages: null,
        csPImage: null,
        csPrice: null,
        csPriceQualifier: null,
        csPurchaseCode: null
      }
    },
    created () {
          this.csTitle = locJSON.CatalogEntryView[0].title,
          this.csPImage = locJSON.CatalogEntryView[0].Images[0].PrimaryImage[0].image,
          this.csAImages = locJSON.CatalogEntryView[0].Images[0].AlternateImages,
          this.csPrice = locJSON.CatalogEntryView[0].Offers[0].OfferPrice[0].formattedPriceValue,
          this.csPriceQualifier = locJSON.CatalogEntryView[0].Offers[0].OfferPrice[0].priceQualifier,
          this.csPurchaseCode = locJSON.CatalogEntryView[0].purchasingChannelCode
    },
    computed : {
      availOnline(){
        return (this.csPurchaseCode == 0 || this.csPurchaseCode == 1)
      },
      availInstore(){
        return (this.csPurchaseCode == 0 || this.csPurchaseCode == 2)
      }
    }
  }

</script>




<style>
  /*reset*/
  /* ref: http://meyerweb.com/eric/tools/css/reset/  */
  html, body, div, span, applet, object, iframe,
  h1, h2, h3, h4, h5, h6, p, blockquote, pre,
  a, abbr, acronym, address, big, cite, code,
  del, dfn, em, img, ins, kbd, q, s, samp,
  small, strike, strong, sub, sup, tt, var,
  b, u, i, center,
  dl, dt, dd, ol, ul, li,
  fieldset, form, label, legend,
  table, caption, tbody, tfoot, thead, tr, th, td,
  article, aside, canvas, details, embed,
  figure, figcaption, footer, header, hgroup,
  menu, nav, output, ruby, section, summary,
  time, mark, audio, video {
  	margin: 0;
  	padding: 0;
  	border: 0;
  	font-size: 100%;
  	font: inherit;
  	vertical-align: baseline;
  }
  /* HTML5 display-role reset for older browsers */
  article, aside, details, figcaption, figure,
  footer, header, hgroup, menu, nav, section {
  	display: block;
  }
  body {
  	line-height: 1;
  }
  ol, ul {
  	list-style: none;
  }
  blockquote, q {
  	quotes: none;
  }
  blockquote:before, blockquote:after,
  q:before, q:after {
  	content: '';
  	content: none;
  }
  table {
  	border-collapse: collapse;
  	border-spacing: 0;
  }



  h1{
    font-weight: 300;
    font-size: 1.55em;
    padding: 0 10%;
    margin: 0 0 .5em;
    line-height: 1.2;
  }

  #app {
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;

    text-align: center;
    color: #000;

    flex-direction: column;
    flex-wrap: wrap;
  }

  ul {
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
    border: 1px solid black;
  }

  .appWrapper{
    display: flex;
    justify-content: center;
  }
  .prodMain{
    width: 480px;
  }
  .prodDetails{
  }
  .purchaseWrapper{
    padding: 1.5em 0;
  }

  .price{
    text-align: left;
    font-family: Arial, sans-serif;
    padding-bottom: 2em;
  }
  .priceValue{
    font-size: 1.65em;
    font-weight: bold;
  }
  .priceQualifier{
    font-size: .7em;
    color: #666666;
  }


@media only screen and (min-width: 1024px) {
    #app {
      flex-direction: row;
      width: 1024px;
      margin: 0 auto;
    }
    .prodMain{
      float: left;
    }
    .prodDetails{
      float: right;
    }
    .prodRatings{
      float: left;
    }
}


</style>
