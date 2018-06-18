<template>
  <div class="appWrapper">
    <div id="app">
      <div class="prodMain">
      <h1 id="prodTitle">{{ csTitle }}</h1>
      <div id="primaryImage" class="blender">
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
        <div v-if="bothAvail" class="shopButton storeButton">Pick Up in Store</div>
        <div v-if="availInstore" class="shopButton storeButton soloButton">Pick Up in Store</div>
        <div v-if="bothAvail" class="shopButton cartButton">Add to Cart</div>
        <div v-if="availInstore" class="shopButton cartButton soloButton">Add to Cart</div>
      </div>

      <div>
        <img src="./assets/mock2b.png">
        <div class="prodHilites">
          <h2>Product Highlights</h2>
          <ul>
            <li>Wattage Output: 1100 Watts</li>
            <li>Number of Speeds: 3</li>
            <li>Capacity (volume): 72.0 Oz.</li>
            <li>Appliance Capabilities: Blends</li>
            <li>Includes: Travel Lid</li>
            <li>Material: Plastic</li>
            <li>Finish: Painted</li>
            <li>Metal Finish: Chrome</li>
            <li>Safety and Security Features: Non-Slip Base</li>
            <li>Care and Cleaning: Easy-To-Clean, Dishwasher Safe Parts</li>
          </ul>
        </div>
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
      bothAvail(){
        return (this.csPurchaseCode == 0);
      },
      availOnline(){
        return (this.csPurchaseCode == 1);
      },
      availInstore(){
        return (this.csPurchaseCode == 2);
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
    position: relative;
    z-index: 100;
  }
  h2{
    font-size: 2.25em;
    text-transform: lowercase;
    line-height: 3.125em
  }

  #app {
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    padding-top: 10em;

    text-align: center;
    color: #000;

    flex-direction: column;
    flex-wrap: wrap;
  }

  .appWrapper{
    display: flex;
    justify-content: center;
  }
  .prodMain{
    width: 480px;
    perspective: 1200px;
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

  .prodHilites{
    font-family: Helvetica;
    text-align: left;
    padding-left: 1.5em;
    line-height: 1.5em;
  }

  .prodHilites ul{
    color: #666;
    font-size: .875em;
    list-style-position: inside;
    list-style-type: disc;
  }


  /*Buttons*/
  .shopButton {
    border-style: solid;
    border-width: 1px;
    border-radius: 3px;
    box-shadow: 0px 1px 2px 0px rgba(0, 0, 0, 0.5);
    width: 13.63em;
    color: #fff;
    font-weight: 100;
    font-size: 1.1em;
    line-height: 2.27em;
    letter-spacing: .08em;
    display: inline-block;
    text-transform: uppercase;
  }
  .cartButton {
    border-color: rgb(204, 0, 0);
    background-color: rgb(204, 0, 0);
    background: linear-gradient(#e16767, #cd0404, #cc0000);
  }
  .storeButton {
    border-color: rgb(0, 0, 0);
    background-color: rgb(204, 0, 0);
    background: linear-gradient(#6a6a6a, #030303, #000);
  }
  .soloButton{
    width: 100%;
  }

  .blender {
    animation-name: spinAnimIn;
    animation-iteration-count: 1;
    animation-timing-function: ease-out;
    animation-duration: 4s;
    animation-fill-mode: forwards;
    transform-style: preserve-3d;
    z-index: 1;
    opacity: 0;

  }

  @keyframes spinAnimIn {
    from { transform: rotateY(360deg);}
    to   { transform: rotateY(0deg);  opacity: 1;}
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
