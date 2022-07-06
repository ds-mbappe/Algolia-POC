<template>
  <ais-instant-search index-name="todos" :search-client="searchClient">
    <div class="video-bg">
      <video autoplay loop muted>
        <source
          src="https://assets.codepen.io/3364143/7btrrd.mp4"
          type="video/mp4"
        />
      </video>
    </div>
    <ais-search-box
      :class-names="{
        'ais-search-box': 'ais-search-box',
      }"
      placeholder="Search something here..."
    />
    <div class="left-panel">
      <!-- <h1>Brands ||</h1> -->
      <ais-refinement-list attribute="brand" show-more />
      <ais-configure :hitsPerPage="8" />
    </div>
    <div class="right-panel">
      <ais-hits
        :class-names="{
          'ais-Hits': 'MyHits',
          'ais-Hits-list': 'MyHitsList',
          'ais-Hits-item': 'MyHitsItem',
        }"
      >
        <template v-slot:item="{ item }">
          <div class="wrapper">
            <div class="card">
              <div class="front">
                <h2>{{ item.name }}</h2>
              </div>
              <div class="right"></div>
            </div>
            <div class="img-wrapper">
              <img
                :src="
                  item.image['thumbnail']
                    ? item.image['thumbnail']
                    : 'https://freepngimg.com/thumb/categories/627.png'
                "
                align="left"
                :alt="item.name"
              />
            </div>
          </div>
        </template>
      </ais-hits>
      <ais-pagination
        :show-first="false"
        :show-previous="false"
        :show-next="false"
        :show-last="false"
      />
    </div>
  </ais-instant-search>
</template>


<script>
import algoliasearch from "algoliasearch/lite";
//import "instantsearch.css/themes/satellite-min.css";

export default {
  props: ["dataImage"],
  data: () => ({
    searchClient: algoliasearch(
      process.env.VUE_APP_APP_ID,
      process.env.VUE_APP_API_KEY
    ),
  }),
  computed: {},
  methods: {},
};
</script>

<style>
body {
  font-family: sans-serif;
  background-image: url("https://assets.codepen.io/3364143/7btrrd.mp4");
}

.video-bg {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: -5;
  width: 100%;
  height: 100%;
}

.video-bg video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.left-panel {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.left-panel h2 {
  margin-left: 3em;
  color: white;
}

.ais-RefinementList-item--selected {
  color: rgb(241, 119, 119);
}

.ais-RefinementList-checkbox {
  border-radius: 50%;
}

.ais-RefinementList-label {
  width: 125%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.right-panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.wrapper {
  width: 280px;
  height: 480px;
  perspective: 800px;
  position: relative;
}

.card {
  width: 240px;
  height: 320px;
  position: relative;
  transform-style: preserve-3d;
  transform: translateZ(-140px);
  transition: transform 350ms cubic-bezier(0.39, 0.575, 0.565, 1);
  cursor: pointer;
}

.card > div {
  position: absolute;
  width: 240px;
  height: 320px;
  padding: 34px 21px;
  transition: all 350ms cubic-bezier(0.39, 0.575, 0.565, 1);
}

.front {
  transform: rotateY(0deg) translateZ(160px);
  border-radius: 24px 3px 0 0;
  box-shadow: rgba(255, 255, 255, 0.66) 0 10px 20px 0,
    inset rgb(255, 255, 255) 0 0 0 2px, inset rgba(255, 255, 255, 0.5) 0 0 0 2px;
  transition: 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
}

.right {
  opacity: 0.08;
  transform: rotateY(90deg) translateX(20px) translateZ(160px);
  border-radius: 0 0 3px 24px;
  box-shadow: rgba(255, 255, 255, 0.66) 0 10px 20px 0,
    inset rgb(255, 255, 255) 0 0 0 2px, inset rgba(255, 255, 255, 0.5) 0 0 0 2px;
  transition: 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
}

.card:hover {
  transform: translateZ(-160px) rotateY(-90deg);
}

.card:hover .front {
  opacity: 0;
}

.card:hover .right {
  opacity: 1;
}

h2 {
  font-size: 21px;
  color: white;
  transform: translateX(20px) translateY(200px);
}

img {
  width: 15em;
  height: 15em;
  transform-origin: top;
  transition: transform 300ms cubic-bezier(0.39, 0.575, 0.565, 1);
  transition-delay: 100ms;
  transform: rotateZ(13deg) skewX(3deg);
  pointer-events: none;
}

.img-wrapper {
  animation: float 4s cubic-bezier(0.39, 0.575, 0.565, 1) infinite alternate;
  position: absolute;
  top: 0;
  right: 0;
  pointer-events: none;
  backface-visibility: hidden;
}

@keyframes float {
  0% {
    transform: translateZ(20px);
  }
  100% {
    transform: translateY(-21px) translateX(-13px) translateZ(30px);
  }
}

.card:hover ~ .img-wrapper img {
  transform: scale(1.1) translateX(47%) translateY(70%) rotateZ(80deg);
}

.MyHitsList {
  display: grid;
  gap: 5em;
  grid-template-rows: repeat(2, 22em);
  grid-template-columns: repeat(4, 15em);
  margin-top: 0;
  margin-right: 5em;
  margin-bottom: 2.5em;
}

.MyHitsItem {
  position: relative;
  display: flex;
  flex-direction: column;
  border-radius: 0.5em;
  transition: 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
  transform: perspective(800px);
  transform-style: preserve-3d;
}

.ais-RefinementList-list {
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

.ais-RefinementList-item {
  margin: 2em;
}

.ais-RefinementList-label {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  transition: 0.25s all ease-in-out;
}

.ais-RefinementList-label:hover {
  cursor: pointer;
  color: rgb(241, 119, 119);
  font-weight: bold;
  transform: scale(1.1);
}

.ais-RefinementList-count {
  display: none;
  background-color: rgb(227, 224, 224);
  border-radius: 5em;
  padding: 0.5em;
}

.ais-RefinementList-item--selected {
  font-weight: bold;
}

.ais-RefinementList-checkbox {
  width: 1em;
  height: 1em;
  border-radius: 50%;
}

.ais-RefinementList-showMore {
  display: none;
}

.ais-SearchBox-submit,
.ais-SearchBox-reset {
  display: none;
}

.ais-SearchBox-input {
  margin-top: 4em;
  text-align: center;
  width: 50em;
  height: 3em;
  border-radius: 2.5em;
}

.ais-InstantSearch {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.hit-name {
  margin-bottom: 0.5em;
}

.hit-description {
  color: #888;
  font-size: 0.8em;
  margin-bottom: 0.5em;
}

.ais-Pagination-list {
  list-style-type: none;
  display: flex;
  flex-direction: row;
}

.ais-Pagination-item {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 2.5em;
  height: 2.5em;
  margin: 1em;
  border-radius: 50%;
  background-color: #000000;
  margin-top: 2em;
  margin-bottom: 2em;
  transition: 0.2s all ease-in-out;
}

.ais-Pagination-item:hover {
  transform: scale(1.25);
  cursor: pointer;
}

.ais-Pagination-link {
  text-decoration: none;
  font-size: 1.5em;
  color: white;
}

.ais-Pagination-item--selected {
  font-weight: bold;
  background-color: rgb(241, 119, 119);
}
</style>
